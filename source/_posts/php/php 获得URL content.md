---
title: php获得url内容的方式
date: 2017-05-19 16:53:00
categories: php
tags:
	- php
---
# php 获得URL content

```
<?php
$url = 'http://www.baidu.com';
$res = getUrlContentByCurl($url);
var_dump($res);
$res = getUrlContentByFopen($url);
var_dump($res);
$res = getUrlContentByfsockOpen($url);
var_dump($res);
$res = getUrlContentByFileGetContents($url);
var_dump($res);
$res = getUrlContentByFile($url);
var_dump($res);

function getUrlContentByFile($url)
{
  $res = file($url);
  return implode('',$res);
}

function getUrlContentByFileGetContents($url) {
  return file_get_contents($url);
}
function getUrlContentByfsockOpen($url)
{
  $url = str_replace('http://', '', $url);
  $res = '';
  $fp = fsockopen($url,80, $errno, $errstr, 30);
  $out = "GET / HTTP/1.1\r\n";
  $out .= "Host: $url\r\n";
  $out .= "Connection: Close\r\n\r\n";
  fwrite($fp, $out);
  while (!feof($fp))
  {
    $res .=  fgets($fp);
  }
  return $res;
}
function getUrlContentByFopen($url)
{
  $fp = fopen($url, 'r');
  $res = '';
  while(!feof($fp)) {
    $res .= fgets($fp);
  }
  return $res;
}


function getUrlContentByCurl($url)
{
  $ch = curl_init();
  curl_setopt($ch, CURLOPT_URL, $url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
  $res = curl_exec($ch);
  return $res;
}
```