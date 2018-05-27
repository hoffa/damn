# 😽 kitten

[![Build Status](https://travis-ci.org/hoffa/damn.svg?branch=master)](https://travis-ci.org/hoffa/damn) [![Maintainability](https://api.codeclimate.com/v1/badges/c47c16854e850f077fbb/maintainability)](https://codeclimate.com/github/hoffa/awsutil/maintainability) [![PyPI - Python Version](https://img.shields.io/pypi/pyversions/kitten.svg)](https://pypi.org/project/kitten) [![PyPI](https://img.shields.io/pypi/v/kitten.svg)](https://pypi.python.org/pypi/kitten) [![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fhoffa%2Fdamn.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fhoffa%2Fdamn?ref=badge_shield)

Tiny tool to manage multiple servers.

## Install

```
pip install kitten
```

## Examples

Get IPs in Auto Scaling group:

```
$ kitten aws asg my-asg-name
18.105.107.20
34.229.135.48
```

Run command on all instances in the Auto Scaling group:

```
$ kitten aws asg my-asg-name | xargs kitten ssh uptime ubuntu
18.105.107.20 uptime
34.229.135.48 uptime
18.105.107.20 17:11:48 up 1 day,  6:02,  0 users,  load average: 0.91, 2.99, 3.49
34.229.135.48 17:11:48 up 5 days, 11:19,  0 users,  load average: 6.34, 5.94, 5.72
```

Commands are always run in parallel. Use `xargs`'s `-L` to not overwhelm your host.

Run command on 10 instances at a time:
```
$ kitten aws asg big-prod-asg | xargs -L 10 kitten ssh --sudo 'service nginx restart' ubuntu
```
