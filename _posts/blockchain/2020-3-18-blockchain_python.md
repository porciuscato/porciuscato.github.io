---
title: 파이썬으로 blockchain을 간단하게 구현해보자.
published: false
updated: 2020-3-18
tags: [python, blockchain]
categories: [development]
---

파이썬으로 구현해보는 블록체인



# Blockchain

파이썬으로 작성한 코드를 참고하여 이를 분석해보고자 한다. 이 코드의 저자는 [Daniel Van Flymen](https://github.com/dvf/blockchain)이다. 코드는 다음과 같다.

## 코드 전체

```python
import hashlib
import json
from time import time
from urllib.parse import urlparse
from uuid import uuid4

import requests
from flask import Flask, jsonify, request


class Blockchain:
    def __init__(self):
        self.current_transactions = []
        self.chain = []
        self.nodes = set()

        # Create the genesis block
        self.new_block(previous_hash='1', nonce=100)

    def register_node(self, address):
        """
        Add a new node to the list of nodes
        :param address: Address of node. Eg. 'http://192.168.0.5:5000'
        """

        parsed_url = urlparse(address)
        if parsed_url.netloc:
            self.nodes.add(parsed_url.netloc)
        elif parsed_url.path:
            # Accepts an URL without scheme like '192.168.0.5:5000'.
            self.nodes.add(parsed_url.path)
        else:
            raise ValueError('Invalid URL')


    def valid_chain(self, chain):
        """
        Determine if a given blockchain is valid
        :param chain: A blockchain
        :return: True if valid, False if not
        """

        last_block = chain[0]
        current_index = 1

        while current_index < len(chain):
            block = chain[current_index]
            print(f'{last_block}')
            print(f'{block}')
            print("\n-----------\n")
            # Check that the hash of the block is correct
            last_block_hash = self.hash(last_block)
            if block['previous_hash'] != last_block_hash:
                return False

            # Check that the Proof of Work is correct
            if not self.valid_nonce(last_block['nonce'], block['nonce'], last_block_hash):
                return False

            last_block = block
            current_index += 1

        return True

    def resolve_conflicts(self):
        """
        This is our consensus algorithm, it resolves conflicts
        by replacing our chain with the longest one in the network.
        :return: True if our chain was replaced, False if not
        """

        neighbours = self.nodes
        new_chain = None

        # We're only looking for chains longer than ours
        max_length = len(self.chain)

        # Grab and verify the chains from all the nodes in our network
        for node in neighbours:
            response = requests.get(f'http://{node}/chain')

            if response.status_code == 200:
                length = response.json()['length']
                chain = response.json()['chain']

                # Check if the length is longer and the chain is valid
                if length > max_length and self.valid_chain(chain):
                    max_length = length
                    new_chain = chain

        # Replace our chain if we discovered a new, valid chain longer than ours
        if new_chain:
            self.chain = new_chain
            return True

        return False

    def new_block(self, nonce, previous_hash):
        """
        Create a new Block in the Blockchain
        :param nonce: The nonce given by the Proof of Work algorithm
        :param previous_hash: Hash of previous Block
        :return: New Block
        """

        block = {
            'index': len(self.chain) + 1,
            'timestamp': time(),
            'transactions': self.current_transactions,
            'nonce': nonce,
            'previous_hash': previous_hash or self.hash(self.chain[-1]),
        }

        # Reset the current list of transactions
        self.current_transactions = []

        self.chain.append(block)
        return block

    def new_transaction(self, sender, recipient, amount):
        """
        Creates a new transaction to go into the next mined Block
        :param sender: Address of the Sender
        :param recipient: Address of the Recipient
        :param amount: Amount
        :return: The index of the Block that will hold this transaction
        """
        self.current_transactions.append({
            'sender': sender,
            'recipient': recipient,
            'amount': amount,
        })

        return self.last_block['index'] + 1

    @property
    def last_block(self):
        return self.chain[-1]

    @staticmethod
    def hash(block):
        """
        Creates a SHA-256 hash of a Block
        :param block: Block
        """

        # We must make sure that the Dictionary is Ordered, or we'll have inconsistent hashes
        block_string = json.dumps(block, sort_keys=True).encode()
        return hashlib.sha256(block_string).hexdigest()

    def proof_of_work(self, last_block):
        """
        Simple Proof of Work Algorithm:
         - Find a number p' such that hash(pp') contains leading 4 zeroes
         - Where p is the previous nonce, and p' is the new nonce
         
        :param last_block: <dict> last Block
        :return: <int>
        """

        last_nonce = last_block['nonce']
        last_hash = self.hash(last_block)

        nonce = 0
        while self.valid_nonce(last_nonce, nonce, last_hash) is False:
            nonce += 1

        return nonce

    @staticmethod
    def valid_nonce(last_nonce, nonce, last_hash):
        """
        Validates the nonce
        :param last_nonce: <int> Previous nonce
        :param nonce: <int> Current nonce
        :param last_hash: <str> The hash of the Previous Block
        :return: <bool> True if correct, False if not.
        """

        guess = f'{last_nonce}{nonce}{last_hash}'.encode()
        guess_hash = hashlib.sha256(guess).hexdigest()
        return guess_hash[:4] == "0000"


# Instantiate the Node
app = Flask(__name__)

# Generate a globally unique address for this node
node_identifier = str(uuid4()).replace('-', '')

# Instantiate the Blockchain
blockchain = Blockchain()


@app.route('/mine', methods=['GET'])
def mine():
    # We run the proof of work algorithm to get the next nonce...
    last_block = blockchain.last_block
    nonce = blockchain.proof_of_work(last_block)

    # We must receive a reward for finding the nonce.
    # The sender is "0" to signify that this node has mined a new coin.
    blockchain.new_transaction(
        sender="0",
        recipient=node_identifier,
        amount=1,
    )

    # Forge the new Block by adding it to the chain
    previous_hash = blockchain.hash(last_block)
    block = blockchain.new_block(nonce, previous_hash)

    response = {
        'message': "New Block Forged",
        'index': block['index'],
        'transactions': block['transactions'],
        'nonce': block['nonce'],
        'previous_hash': block['previous_hash'],
    }
    return jsonify(response), 200


@app.route('/transactions/new', methods=['POST'])
def new_transaction():
    values = request.get_json()

    # Check that the required fields are in the POST'ed data
    required = ['sender', 'recipient', 'amount']
    if not all(k in values for k in required):
        return 'Missing values', 400

    # Create a new Transaction
    index = blockchain.new_transaction(values['sender'], values['recipient'], values['amount'])

    response = {'message': f'Transaction will be added to Block {index}'}
    return jsonify(response), 201


@app.route('/chain', methods=['GET'])
def full_chain():
    response = {
        'length': len(blockchain.chain),
        'chain': blockchain.chain,
    }
    return jsonify(response), 200


@app.route('/nodes/register', methods=['POST'])
def register_nodes():
    values = request.get_json()
    nodes = values.get('nodes')
    if nodes is None:
        return "Error: Please supply a valid list of nodes", 400

    for node in nodes:
        blockchain.register_node(node)

    response = {
        'message': 'New nodes have been added',
        'total_nodes': list(blockchain.nodes),
    }
    return jsonify(response), 201


@app.route('/nodes/resolve', methods=['GET'])
def consensus():
    replaced = blockchain.resolve_conflicts()

    if replaced:
        response = {
            'message': 'Our chain was replaced',
            'new_chain': blockchain.chain
        }
    else:
        response = {
            'message': 'Our chain is authoritative',
            'chain': blockchain.chain
        }

    return jsonify(response), 200


if __name__ == '__main__':
    from argparse import ArgumentParser

    parser = ArgumentParser()
    parser.add_argument('-p', '--port', default=5000, type=int, help='port to listen on')
    args = parser.parse_args()
    port = args.port

    app.run(host='127.0.0.1', port=port)
```

이 코드를 실행하면 flask 서버가 실행되고 localhost에서 get 요청을 통해 채굴을 하거나 체인의 정보를 가져올 수 있다.

이를 하나씩 분석해보자.

## 코드 분석

위 코드는 크게 두 부분으로 나뉜다. 하나는 블록체인을 정의하고, 하나는 flask 서버를 정의한다. 각각을 나눠서 살펴보자.

### 블록체인 클래스

이 클래스의 속성과 메소드는 다음과 같다.

| 속성                      | 설명                                                         |
| ------------------------- | ------------------------------------------------------------ |
| self.current_transacionts | 블록 생성된 이후 발생한 트랜잭션들에 대한 기록이다. 리스트 타입이며 트랜잭션이 생성될 때마다 추가된다. 블록이 새로 생성되면 이 트랜잭션은 초기화된다. |
| self.chain                | 현재까지 만들어진 모든 블럭들에 대한 기록이다. 리스트 타입이며 모든 블럭을 담고 있다. |
| self.nodes                | 트랜잭션을 발생시킬 수 있는 주체들에 대한 정보다. 현재는 중복되지 않는 이름들만 저장한다. |
| self.new_block            | 제네시스 블록이다. hash는 1, nonce는 100으로 설정되어 있다.  |

| 메소드                                                 | 매개변수                                                     | 반환  | 설명                                                         |
| ------------------------------------------------------ | ------------------------------------------------------------ | ----- | ------------------------------------------------------------ |
| register_node<br />(self, address)                     | - address: 노드의 주소다.                                    | X     | 받은 주소를 이름으로 하는 노드를 생성한다.                   |
| valid_chain<br />(self, chain)                         | - chain: 전달 받은 체인이다.                                 | Bool  | 전달받은 체인을 검증한다. 처음부터 마지막 노드까지 검증하며 타당할 경우 참을 반환한다. |
| resolve_conflicts<br />(self)                          | X                                                            | Bool  | 합의 알고리즘이다. 체인들 간 충돌을 해결한다. 이때 모든 노드의 체인들을 검사하여 가장 긴 체인을 타당한 것으로  받아들인다. |
| new_block<br />(self, nonce, previous_hash)            | - nonce: POW의 결과값<br />- previous_hash:  이전 블록의 해쉬값 | Block | 새로운 블럭을 생성한다. 블럭에 모든 정보를 담고 current_transaction을 비운다. <br /> |
| new_transaction<br />(self, sender, recipient, amount) | - sender: 보내는 노드<br />- recipient: 받는 노드<br />- amount: 보낼 값 | index | 트랜잭션이 발생하면 이를 저장한다. 원래는 트랜잭션도 검증이 필요하지만 이 코드는 하지 않는다. 반환되는 index는 이 거래가 담길 블록의 인덱스를 의미한다. |
| last_block<br />(self)                                 | X                                                            | Block | 마지막 블럭을 반환한다.                                      |
| hash<br />(block)                                      | - block                                                      | hash  | 이전 블럭의 정보를 모아 해시값을 만든다.                     |
| proof_of_work<br />(self, last_block)                  | -  last_block                                                | nonce | 마지막 블럭의 nonce 값과 해시값으로 새로운 블럭에 들어갈 nonce 값을 찾는다. 0부터 하나씩 더해가며 정수값 nonce를 구한다. |
| valid_nonce<br />(last_nonce, nonce, last_hash)        | - last_nonce: 마지막 블럭의 nonce다.<br />- nonce: 생성할 블럭의 nonce 값이다.<br />- last_hash: 마지막 블럭의 해시값이다. | Bool  | 생성한 nonce 값이 타당한지 검증한다. 타당할 경우 True를 반환한다. |

### Flask

URL 구조는 다음과 같다.

| URL              | method | 설명                                                         |
| ---------------- | ------ | ------------------------------------------------------------ |
| /mine            | GET    | 채굴 요청이다. 마지막 블럭을 가져와 타당한 논스를 구한다. 이후 새로운 블럭이 생성되었다는 트랜잭션을 발생시키고 새로운 블럭을 응답으로 보낸다. |
| /transcation/new | POST   | 트랜잭션을 일으키는 요청이다. 요청은 JSON 형식으로 보내야 하며, sender, recipient, amount를 key로 가진다. |
| /chain           | GET    | 현재까지의 체인을 볼 수 있다.                                |
| /nodes/register  | POST   | 새로운 사용자를 추가한다. JSON 형식으로 보낸다.              |
| /nodes/resolve   | GET    | 충돌을 해결하는 요청이다. 모든 노드들과 연결된 블럭들을 검사하며 가장 긴 체인을 타당한 것으로 여긴다. |

