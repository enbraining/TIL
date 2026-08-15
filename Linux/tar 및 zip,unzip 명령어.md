# tar 및 zip/unzip 명령어

각 명령어의 사용법을 설명하기에 앞서 차이점을 먼저 설명하려 합니다.

tar 명령어는 대상 파일들을 하나의 스트림으로 순서대로 이어붙이고, 전체 스트림을 한번에 gzip/bzip2/xz로 압축하는 방식을 사용합니다.

반면, zip 명령어는 대상 파일들을 각각 압축하고 이를 모아 컨테이너로 만듭니다.

# tar 명령어

tar 명령어는 gzip, xz 등 다양한 압축 방식을 지원합니다. 

주로 사용하게 될 명령어는 아래와 같습니다.

```bash
tar -czvf   # gzip (.tar.gz / .tgz) — 가장 흔함, 빠름
tar -cjvf   # bzip2 (.tar.bz2) — 압축률 더 좋지만 느림
tar -cJvf   # xz (.tar.xz) — 압축률 최고, 요즘 배포판 소스에서 자주 봄
```

옵션에서 첫번째는 c(create), x(extract), t(list)를 넣고, 두번째는 압축 유형에 따라 z/j/J를 넣어주면 됩니다.

이후 옵션들은 아래와 같습니다.

- v(verbose): 처리 중인 파일 목록을 화면에 출력
- f(file): 바로 뒤에 오는 인자가 아카이브 파일명이라는 뜻 (무조건 맨 뒤)

아래는 사용 예시입니다.

```bash
tar -czvf backup.tar.gz /etc/nginx # /etc/nginx 경로를 backup.tar.gz로 압축
tar -xzvf backup.tar.gz # backup.tar.gz를 압축 해제
tar -xzvf backup.tar.gz -C /test # /test 경로에 압축 해제
```

# zip/unzip 명령어

zip 명령어는 tar와 달리 별도 압축 방식 지정이 필요 없습니다. 자체적으로 압축 알고리즘이 내장되어 있기 때문입니다.

```bash
zip -r archive.zip ~/test # 압축 (디렉토리를 압축 시 -r을 추가해 재귀적으로 포함해야 함)
unzip archive.zip # 현재 경로에 압축 해제
unzip archive.zip -d ~/test # ~/test 경로에 압축 해제
unzip -l archive.zip # 풀지 않고 내부 파일 목록만 확인
```

