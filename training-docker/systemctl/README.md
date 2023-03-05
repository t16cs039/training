## 概要

Dockerコンテナ内でsystemctlコマンドを実行する方法について調べる

- [追記参考文献](https://qiita.com/ryysud/items/e6bfd61a121d6f922288)

## 追記

- dockerコマンドを打つ際にsudoコマンドを打たないと実行不可にする方法

- cent7でも動作することを確認しました。

```shell
$ sudo chown root  .docker/run/docker.sock
```

- centos:8に変更

- 以後精査していく必要がある

```shell
$ docker run -itd --rm --name test --privileged=true --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw test-image "/sbin/init"
```

- [Docker for mac (ver 4.3以降)で「Failed to get D-Bus connection」](https://qiita.com/NaoyaMiyagawa/items/22a870112377a91e1c99)

## 結論

- 出来ない気がするなぁ

- [Unable to run systemd services on Docker Desktop 4.3.0](https://github.com/docker/for-mac/issues/6073)

## 検証方法

- 基本的な一連の流れ

```shell
$ docker build . -t test-image

$ docker run -d -t --name test test-image

$ docker container exec -it test bash

# systemctl list-units --type=service
```

- 下記記事を参考

    - 結論から述べると、失敗する

    - `--priviledged`オプションと`/sbin/init`で立ち上げる

    - [CentOS7のDockerコンテナでsystemctlを使えるようにする](https://qiita.com/mikene_koko/items/4c71c969f55e3fe24190)

```shell
$ docker run -d -t --privileged --name test test-image /sbin/init

$ systemctl list-units --type=service
Failed to get D-Bus connection: No such file or directory
```

- 上記記事コマンドを参考

    - 結論から述べると、失敗する

```shell
$ docker run -it -v /sys/fs/cgroup:/sys/fs/cgroup:ro --cap-add SYS_ADMIN test-container /sbin/init
Failed to mount cgroup at /sys/fs/cgroup/systemd: No such file or directory
systemd 219 running in system mode. (+PAM +AUDIT +SELINUX +IMA -APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 -SECCOMP +BLKID +ELFUTILS +KMOD +IDN)
Detected architecture arm64.

Welcome to CentOS Linux 7 (AltArch)!

Set hostname to <8193524afd0a>.
Initializing machine ID from random generator.
Cannot determine cgroup we are running in: No such file or directory
Failed to allocate manager object: No such file or directory
[!!!!!!] Failed to allocate manager object, freezing.
```
