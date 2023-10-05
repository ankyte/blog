---
author: Ankit Sahu
pubDatetime: 2023-08-23T00:00:00Z
title: Installing ML-Agents on macOS M1 ( A Troubleshooting Guide ) 👨‍💻
postSlug: mlagents-installation-troubleshoot
featured: true
draft: false
tags:
  - unity
  - python
  - macos
  - reinforcement_learning
description: If you're an AI and ML enthusiast like me, you might have encountered challenges while trying to install the ML-Agents Python library on your Mac M1. Fear not, I've gone through the pains 🥲👍 and want to share my experience to make this process smoother for you. 🤖
---

If you're an AI and ML enthusiast like me, you might have encountered challenges while trying to install the ML-Agents Python library on your Mac M1. Fear not, I've gone through the pains 🥲👍 and want to share my experience to make this process smoother for you. 🤖

## Table of contents

## Step 1: Creating a Virtual Environment

First, let's create a virtual environment using the `venv` tool. Open your terminal and execute the following command:

```bash
python -m venv rl-env
```

## Step 2: Installing ML-Agents

Now, let's install ML-Agents using `pip`. Run this command within your virtual environment:

```bash
python -m pip install mlagents==0.30.0
```

## Step 3: Checking Installation

To ensure ML-Agents is correctly installed, run the following command:

```bash
mlagents-learn --help
```

If you encounter no errors, consider yourself lucky 🦄!
But, if you face an error like the one below, don't worry, I've got your back 😎.

```bash
Traceback (most recent call last):
  File "/Users/alpha/miniforge3/envs/rl-venv/bin/mlagents-learn", line 5, in <module>
    from mlagents.trainers.learn import main
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents/trainers/learn.py", line 2, in <module>
    from mlagents import torch_utils
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents/torch_utils/__init__.py", line 1, in <module>
    from mlagents.torch_utils.torch import torch as torch  # noqa
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents/torch_utils/torch.py", line 6, in <module>
    from mlagents.trainers.settings import TorchSettings
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents/trainers/settings.py", line 25, in <module>
    from mlagents.trainers.cli_utils import StoreConfigFile, DetectDefault, parser
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents/trainers/cli_utils.py", line 5, in <module>
    from mlagents_envs.environment import UnityEnvironment
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents_envs/environment.py", line 12, in <module>
    from mlagents_envs.side_channel.side_channel import SideChannel
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents_envs/side_channel/__init__.py", line 5, in <module>
    from mlagents_envs.side_channel.default_training_analytics_side_channel import (  # noqa
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents_envs/side_channel/default_training_analytics_side_channel.py", line 7, in <module>
    from mlagents_envs.communicator_objects.training_analytics_pb2 import (
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/mlagents_envs/communicator_objects/training_analytics_pb2.py", line 35, in <module>
    _descriptor.FieldDescriptor(
  File "/Users/alpha/miniforge3/envs/rl-venv/lib/python3.9/site-packages/google/protobuf/descriptor.py", line 561, in _new_
    _message.Message._CheckCalledFromGeneratedFile()
TypeError: Descriptors cannot not be created directly.
If this call came from a _pb2.py file, your generated code is out of date and must be regenerated with protoc >= 3.19.0.
If you cannot immediately regenerate your protos, some other possible workarounds are:
 1. Downgrade the protobuf package to 3.20.x or lower.
 2. Set PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python (but this will use pure-Python parsing and will be much slower).

More information: https://developers.google.com/protocol-buffers/docs/news/2022-05-06#python-updates
```

## Step 4: Downgrading Protobuf

To fix the protobuf issue, you need to downgrade it. Run the following command:

```bash
pip install protobuf==3.20.0
```

## Step 5: Rechecking Installation

Now, check if ML-Agents is installed correctly again:

```bash
mlagents-learn --help
```

## Step 6: Addressing Further Errors

You might encounter another error related to symbol not found in flat namespace '\_CFDataGetBytes'. This is due to the CoreFoundation framework not being available on Apple Silicon Macs by default.

```bash
Traceback (most recent call last):
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/bin/mlagents-learn", line 33, in <module>
    sys.exit(load_entry_point('mlagents==0.30.0', 'console_scripts', 'mlagents-learn')())
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/bin/mlagents-learn", line 25, in importlib_load_entry_point
    return next(matches).load()
  File "/Users/alpha/miniforge3/lib/python3.10/importlib/metadata/__init__.py", line 171, in load
    module = import_module(match.group('module'))
  File "/Users/alpha/miniforge3/lib/python3.10/importlib/__init__.py", line 126, in import_module
    return _bootstrap._gcd_import(name[level:], package, level)
  File "<frozen importlib._bootstrap>", line 1050, in _gcd_import
  File "<frozen importlib._bootstrap>", line 1027, in _find_and_load
  File "<frozen importlib._bootstrap>", line 1006, in _find_and_load_unlocked
  File "<frozen importlib._bootstrap>", line 688, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 883, in exec_module
  File "<frozen importlib._bootstrap>", line 241, in _call_with_frames_removed
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/mlagents/trainers/learn.py", line 2, in <module>
    from mlagents import torch_utils
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/mlagents/torch_utils/__init__.py", line 1, in <module>
    from mlagents.torch_utils.torch import torch as torch  # noqa
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/mlagents/torch_utils/torch.py", line 6, in <module>
    from mlagents.trainers.settings import TorchSettings
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/mlagents/trainers/settings.py", line 25, in <module>
    from mlagents.trainers.cli_utils import StoreConfigFile, DetectDefault, parser
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/mlagents/trainers/cli_utils.py", line 5, in <module>
    from mlagents_envs.environment import UnityEnvironment
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/mlagents_envs/environment.py", line 49, in <module>
    from .rpc_communicator import RpcCommunicator
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/mlagents_envs/rpc_communicator.py", line 1, in <module>
    import grpc
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/grpc/__init__.py", line 22, in <module>
    from grpc import _compression
  File "/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/grpc/_compression.py", line 20, in <module>
    from grpc._cython import cygrpc
ImportError: dlopen(/Users/alpha/Files/dev/reinforcement-learning-unity/rl-env/lib/python3.10/site-packages/grpc/_cython/cygrpc.cpython-310-darwin.so, 0x0002): symbol not found in flat namespace '_CFDataGetBytes'
```

To solve this, rebuild grpcio from source using the following commands:

```bash
pip uninstall grpcio
export GRPC_PYTHON_LDFLAGS=" -framework CoreFoundation"
pip install grpcio --no-binary :all:
```

## Wrapping Up

Congratulations, you've successfully navigated through the installation process! Don't let these hiccups discourage you; troubleshooting is an integral part of a developer's journey.🚀
