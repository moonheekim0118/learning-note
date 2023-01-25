# NPM vs YARN

1. yarn 이 속도가 더 빠르다.
2. Automatic Lock file generation, 자동 lock 파일 생성

   - 종속성이 추가되면 yarn 은 yarn.lock 파일을 자동으로 추가한다.
   - NPM은 npm shrinkwrap 명령어로 lock 파일을 생성한다. (과거에. 현재는 개선되었지만 , yarn의 속도에 못미친다.)
   - lock 파일이란, 프로젝트에 패키지에 최초로 추가될 당시에 정확히 어떤 버전이 설치가 되었는지를 기록한다.

3. 보안

- NPM은 다른 패키지를 즉시 포함시킬 수 있는 코드를 자동으로 실행하므로, 보안 시스템에 여러가지 취약성이 발생한다.
- 반면, yarn은 yarn.lock 또는 pacakge.json 파일에 있는 파일만 설치한다.
