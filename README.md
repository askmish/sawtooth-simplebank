# sawtooth-simplewallet
A simple sawtooth "simplewallet" transaction family example (processor + client)

# simplewallet

This is a minimal example of a sawtooth 1.0 application. This example demonstrates, a common usecase, where a customer deposits/withdraws/transfers money from an account, based on public key.

A customer can:
1. deposit money into his/her bank account.
2. withdraw money from his/her bank account.
3. check the balance in the account.
4. transfer money from one bank account to another

The customer is identified by a customer name and a corresponding public key. The value of the wallet, i.e. the balance, is stored at an address derived from hash of customer's public key and the transaction family namespace.

# Components
The application is built in two parts:
1. The client application written in Python, written in two parts: _client.py file representing the backend stuff and the _cli.py representing the frontend stuff. The example is built by using the setup.py file located in one directory level up.

2. The Transaction Processor is written in C++11 using c++-sawtooth-sdk. It comes with its CMake files for build. The Transaction Processor is also available in Java and Python.

# Usage

This example uses docker-compose and Docker containers. If you do not have these installed please follow the instructions here: https://docs.docker.com/install/

NOTE
The preferred OS environment is Ubuntu 16.04.3 LTS x64.
If you have Windows please install [Docker Toolbox for Windows](https://docs.docker.com/toolbox/toolbox_install_windows/) or [Docker for Windows](https://docs.docker.com/docker-for-windows/), based on your OS version.

Start the pre-built Docker containers in docker-compose.yaml file, located in sawtooth-simplewallet directory:
```bash
cd sawtooth-simplewallet
docker-compose up
```
At this point all the containers should be running.

To launch the client, you could do this:
```bash
docker exec -it simplewallet-client bash
```

You can locate the right Docker client container name using `docker ps`.

Sample command usage:

```bash
#Create a wallet
sawtooth keygen jack #This creates the public/private keys for Jack, a pre-requisite for the following commands

simplewallet deposit 100 jack #This adds 100 units to Jack's account

simplewallet withdraw 50 jack #Withdraws 50 units from Jack's account

simplewallet balance jack #Displays the balance left in Jack's account

#Create 2nd wallet
sawtooth keygen jill #This creates the public/private keys for Jill, a pre-requisite for the following commands

simplewallet deposit 100 jill #This adds 100 units to Jill's account

simplewallet balance jill #Displays the balance left in Jill's account

simplewallet transfer 25 jack jill #Transfer 25 units money from Jack to Jill

simplewallet balance jack #Displays the balance left in Jack's account

simplewallet balance jill #Displays the balance left in Jill's account

```

# Building containers
To build TP code of your preferred language and run the simplewallet example:

```bash
docker-compose -f simplewallet-build-tp-<your_prog_language>.yaml up --build
```
where,
 <your_prog_language> should be replaced with either `cxx`, `java`, or `py`

# Contributing
Currently, we're looking for contributions and PRs for following:
 - TPs using GO and .NET sawtooth SDKs
 - Client apps in GO, .NET, C++, and Java

More ways you can contribute:
 - Bugs or issues: Report problems or defects found when working with simplewallet
 - Core features and enhancements: Provide expanded capabilities or optimizations
 - Documentation: Improve existing documentation or create new information
 - Tests: Add functional, performance, or scalability tests

# License
This example and Hyperledger Sawtooth software are licensed under the [Apache License Version 2.0](LICENSE) software license.
