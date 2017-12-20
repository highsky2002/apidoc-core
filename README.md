# apidoc-core

apidoc支持 -i参数指明要解析的目录, -f参数应用正则的文件匹配过滤器；其中进行-f文件匹配过滤的源串是文件的绝对路径(带文件类型后缀)【不要以为匹配的串是-i目录下的纯文件名】, 写正则表达式时这点需要注意

举样例，录入你想为每一个入口文件生成一个api访问路径, 如下-f 内容中起始的"\/"就显得比较关键，否则输出结果可能多于单个入口文件的内容

<pre><code>
cd /usr/local/nginx/web_modules/action
for dir in $(ls)
do
if [ -d $dir ] && [ ! -L $dir ];then
    for file in $(ls $dir)
    do
        pureName=${file%.*}
        extension=${file##*.}
        if [ $extension == "php" ];then
            #echo $pureName
            apidoc -i /usr/local/nginx/web_modules/action/$dir/ -f "\/$pureName\.php$" -o /usr/local/nginx/web_modules/api/$dir/$pureName
        fi
    done
fi
done
</code></pre>

Core parser library to generate apidoc result following the [apidoc-spec](https://github.com/apidoc/apidoc-spec)

[![Build Status](https://travis-ci.org/apidoc/apidoc-core.svg?branch=master)](https://travis-ci.org/apidoc/apidoc-core)
[![Dependency Status](https://david-dm.org/apidoc/apidoc-core.svg)](https://david-dm.org/apidoc/apidoc-core)
[![NPM version](https://badge.fury.io/js/apidoc-core.svg)](http://badge.fury.io/js/apidoc-core)

If you are an end user, please proceed to [apidoc](https://github.com/apidoc/apidoc) or [apidoc-documentation](http://apidocjs.com).

[Changelog](https://github.com/apidoc/apidoc/blob/master/CHANGELOG.md).
