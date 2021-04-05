# 기술 블로그

[https://jesterz91.github.io](https://jesterz91.github.io)

개발공부 및 개인경험 등을 정리하기 위한 개인 블로그 입니다. 


## Jekyll 환경 설정

### Ruby 설치
```
sudo apt install ruby ruby-dev build-essential
```

### Ruby Gem 설치 디렉토리 설정
```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### Jekyll 및 Bundler 설치
```
gem install jekyll bundler
```

###  의존성 패키지 설치

```
bundle install
```

### 로컬에서 Jekyll 실행

```
bundle exec jekyll serve
```
http://127.0.0.1:4000 접속


***

### Tech

- Generator : [jekyll](https://jekyllrb.com)
- Theme : [centrarium](https://github.com/bencentra/centrarium)
- Syntax highlight : [highlight.js](https://highlightjs.org)
- Overlay images : [lightbox.js](https://lokeshdhakar.com/projects/lightbox2)
- Search : [lurn.js](https://lunrjs.com)
- Tag cloud : [Jason Davies](https://www.jasondavies.com/wordcloud)