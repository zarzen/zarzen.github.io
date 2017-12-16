---
layout: post
title:  "Config Chinese Fonts on Linux Mint 18.2"
date:   2017-10-13 14:47:31
categories: linux mint fonts
---

* Install Fonts: "DejaVu", "WenQuanYi" etc.
* Create/edit `/etc/fonts/conf.avail/69-language-selector-zh-cn.conf` as following:    
content copied from [this-gist](https://gist.github.com/zhangtai/11075224)

``` xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="pattern">
    <test qual="any" name="family">
      <string>serif</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>DejaVu Serif</string>
      <string>Bitstream Vera Serif</string>
      <string>HYSong</string>
      <string>AR PL UMing CN</string>
      <string>AR PL UMing HK</string>
      <string>AR PL ShanHeiSun Uni</string>
      <string>AR PL New Sung</string>
      <string>WenQuanYi Bitmap Song</string>
      <string>AR PL UKai CN</string>
      <string>AR PL ZenKai Uni</string>
    </edit>
  </match>
  <match target="pattern">
    <test qual="any" name="family">
      <string>sans-serif</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>DejaVu Sans</string>
      <string>Bitstream Vera Sans</string>
      <string>WenQuanYi Micro Hei</string>
      <string>WenQuanYi Zen Hei</string>
      <string>Droid Sans Fallback</string>
      <string>HYSong</string>
      <string>AR PL UMing CN</string>
      <string>AR PL UMing HK</string>
      <string>AR PL ShanHeiSun Uni</string>
      <string>AR PL New Sung</string>
      <string>AR PL UKai CN</string>
      <string>AR PL ZenKai Uni</string>
    </edit>
  </match>
  <match target="pattern">
    <test qual="any" name="family">
      <string>monospace</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>DejaVu Sans Mono</string>
      <string>Bitstream Vera Sans Mono</string>
      <string>WenQuanYi Micro Hei Mono</string>
      <string>WenQuanYi Zen Hei Mono</string>
      <string>Droid Sans Fallback</string>
      <string>HYSong</string>
      <string>AR PL UMing CN</string>
      <string>AR PL UMing HK</string>
      <string>AR PL ShanHeiSun Uni</string>
      <string>AR PL New Sung</string>
      <string>AR PL UKai CN</string>
      <string>AR PL ZenKai Uni</string>
    </edit>
  </match>
</fontconfig>
```

* Create a symbolic link at `/etc/fonts/conf.d`
```
cd /etc/fonts/conf.d
sudo ln -s ../conf.avail/69-language-selector-zh-cn.conf 69-language-selector-zh-cn.conf
```