---
toc: true
toc_sticky: true
# toc_label: "Unique Title"
toc_icon: "heart"

title:  "맥북에서 nokogiri gem install 오류 해결"
excerpt: "nokogiri gem with libxml2 error"

categories:
  - it
tags:
  - mac
  - rails
  - problem solving
last_modified_at: 2020-02-04T12:12:00+09:00
---

맥북에서 nokogiri gem install 시에 libxml2 경로를 찾지 못하는 문제 발생함.

## Solution

### in Rails 6
```bash
gem install nokogiri -- --use-system-libraries=true --with-xml2-include="$(xcrun --show-sdk-path)"/usr/include/libxml2
```

### in Rails 5
```
bundle config build.nokogiri --use-system-libraries --with-xml2-include=/usr/local/opt/libxml2/include/libxml2
```

## Error Log

```
Installing nokogiri 1.10.7 with native extensions
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /Users/andrew/.rbenv/versions/2.6.0/lib/ruby/gems/2.6.0/gems/nokogiri-1.10.7/ext/nokogiri
/Users/andrew/.rbenv/versions/2.6.0/bin/ruby -I /Users/andrew/.rbenv/versions/2.6.0/lib/ruby/2.6.0 -r
./siteconf20200204-2474-1u695rc.rb extconf.rb --use-system-libraries\=true\
--with-xml2-include\=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/usr/include/libxml2
checking if the C compiler accepts  -I /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/libxml2... yes
checking if the C compiler accepts -Wno-error=unused-command-line-argument-hard-error-in-future... no
Building nokogiri using system libraries.
ERROR: cannot discover where libxml2 is located on your system. please make sure `pkg-config` is installed.
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
```