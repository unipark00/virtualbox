#### 인증키 등록
```
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
```
#### 크롬 패키지를 다운받을 PPA를 sources.list에 추가
```
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" \
    >> /etc/apt/sources.list.d/google.list'
```
#### 추가한 PPA로부터 설치 가능할 크롬 웹브라우저 패키지 정보를 가져오기 위해 패키지 리스트를 업데이트
```
sudo apt-get update
```
#### 크롬 웹 브라우저를 설치
```
sudo apt-get install google-chrome-stable
```
#### 자동으로 생성된 google-chrome.list 파일
```
ejungpa@ubuntu1:~$ ls /etc/apt/sources.list.d/google*
/etc/apt/sources.list.d/google-chrome.list  /etc/apt/sources.list.d/google.list
```
#### 설치 파일 삭제
```
sudo rm -rf /etc/apt/sources.list.d/google.list
```
