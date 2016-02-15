`locate`는 이름으로 파일을 빠르게 찾는 유닉스 도구이다. 이 도구는 파일 시스템을 직접적인 대상으로 하지 않고 미리 생성된 데이터베이스 파일을 찾기 때문에 [find](http://en.wikipedia.org/wiki/Find) 도구에 비해 속도가 향상되었다. 이 방법의 단점은 데이터베이스 파일이 생성된 후에 생긴 변화는`locate`가 탐지하지 못한다는 점이다. 이 문제는 `updatedb`라는 명령어가 그 이름이 암시하듯이 데이터베이스를 갱신하는 명령어인데 이를 주기적으로 사용하여 문제의 가능성을 줄일 수 있다.

## 설치

다른 배포판에서는 `locate`와 `updatedb`가 [findutils](https://www.archlinux.org/packages/?name=findutils) 꾸러미에 있지만, 아치 꾸러미에는 더 이상 없다. 이를 사용하려면 [mlocate](https://www.archlinux.org/packages/?name=mlocate) 꾸러미를 설치하라. mlocate 꾸러미는 이전의 도구를 더욱 향상시켰으나 사용법은 똑같다.

`locate`를 사용하기에 앞서 데이터베이스를 생성해야 한다. 이를 위해 간단히 `updatedb` 명령어를 루트 권한으로 실행하라.

### 데이터베이스를 최신 상태로 유지하기

When `mlocate`가 설치될 때 데이터베이스를 갱신할 `/etc/cron.daily`( [cron](/index.php/Cron "Cron")이 매일 실행) 스크립트가 자동으로 설치된다. 또한 언제라도 `updatedb`를 수동으로 실행할 수 있다.

시간을 절약하기 위해 `updatedb`는 특정한 파일시스템과 경로를 무시하도록 `/etc/updatedb.conf`를 편집해서 설정할 수 있다. `man updatedb.conf`는 이 파일의 의미를 설명한다. 디폴트 설정 파일에서 무시되는 경로("PRUNEPATHS" 문자열에 지정됨) 중에서 `/media`와 `/mnt`가 있다. 따라서 `locate`는 외부 장치에 있는 파일을 찾지 못할 수도 있다.