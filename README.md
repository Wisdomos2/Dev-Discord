# *Discord chat bot*
## Discord chat bot - 개인서버에서 LOL 전적/간단한 게임 구현.

### Why did i choose this.
- 10대부터 30대까지 자주 사용하는 채팅플랫폼 디스코드에 편의 기능을 추가하기 위함.

### Development Environments.
- Python
- Open Source
- Parsing

### Configuration.
- Open Source와 Web Parsing 을 이용한 게임전적 호출 기능 구현.
- 벌칙 또는 무엇을 정하기 위한 간단한 미니 게임 구현.
- 채팅방에 있는 사용자 호출, 호출 할 때 특정 언급 기능 구현. 

### What did i learn.
- 어떻게 Open Source Customizing 을 하는가.
- Web Parsing 방법.
- Python Server의 개요.

### What to do in the future.
- 채팅방 사용자가 필요하거나 요구하는 기능이 있다면 추가 할 예정.


## discord dev

pyhton 3.6 버전부터됨.

pip install discord.py

pip install --upgrade (필요에 따라) 해줘야함.











































# discord.py

[![PyPI](https://img.shields.io/pypi/v/discord.py.svg)](https://pypi.python.org/pypi/discord.py/)
[![PyPI](https://img.shields.io/pypi/pyversions/discord.py.svg)](https://pypi.python.org/pypi/discord.py/)

discord.py is an API wrapper for Discord written in Python.

This was written to allow easier writing of bots or chat logs. Make sure to familiarise yourself with the API using the [documentation][doc].

[doc]: http://discordpy.rtfd.org/en/latest

### Breaking Changes

The discord API is constantly changing and the wrapper API is as well. There will be no effort to keep backwards compatibility in versions before `v1.0.0`.

I recommend joining either the [official discord.py server][guild] or the [Discord API server][ch] for help and discussion about the library.

[guild]: https://discord.gg/r3sSKJJ
[ch]: https://discord.gg/discord-api

## Installing

To install the library without full voice support, you can just run the following command:

```
python3 -m pip install -U discord.py
```

Otherwise to get voice support you should run the following command:

```
python3 -m pip install -U discord.py[voice]
```

To install the development version, do the following:

```
python3 -m pip install -U https://github.com/Rapptz/discord.py/archive/master.zip#egg=discord.py[voice]
```

or the more long winded from cloned source:

```
$ git clone https://github.com/Rapptz/discord.py
$ cd discord.py
$ python3 -m pip install -U .[voice]
```

Please note that on Linux installing voice you must install the following packages via your favourite package manager (e.g. `apt`, `yum`, etc) before running the above command:

- libffi-dev (or `libffi-devel` on some systems)
- python<version>-dev (e.g. `python3.5-dev` for Python 3.5)

## Quick Example

```py
import discord
import asyncio

client = discord.Client()

@client.event
async def on_ready():
    print('Logged in as')
    print(client.user.name)
    print(client.user.id)
    print('------')

@client.event
async def on_message(message):
    if message.content.startswith('!test'):
        counter = 0
        tmp = await client.send_message(message.channel, 'Calculating messages...')
        async for log in client.logs_from(message.channel, limit=100):
            if log.author == message.author:
                counter += 1

        await client.edit_message(tmp, 'You have {} messages.'.format(counter))
    elif message.content.startswith('!sleep'):
        await asyncio.sleep(5)
        await client.send_message(message.channel, 'Done sleeping')

client.run('token')
```

Note that in Python 3.4 you use `@asyncio.coroutine` instead of `async def` and `yield from` instead of `await`.

You can find examples in the examples directory.

## Requirements

- Python 3.4.2+
- `aiohttp` library
- `websockets` library
- `PyNaCl` library (optional, for voice only)
    - On Linux systems this requires the `libffi` library. You can install in
      debian based systems by doing `sudo apt-get install libffi-dev`.

Usually `pip` will handle these for you.
