# ruby-mp3info

[![Build Status](https://secure.travis-ci.org/moumar/ruby-mp3info.png)](http://travis-ci.org/moumar/ruby-mp3info)

## Description

ruby-mp3info read low-level informations and manipulate tags on
mp3 files.

## Features/problems

* written in pure ruby 
* read low-level informations like bitrate, length, samplerate, etc...
* read, write, remove id3v1 and id3v2 tags
* correctly read VBR files (with or without Xing header)
* only 2.3 version is supported for writings id3v2 tags

## Synopsis

### read and display infos & tags

    require "mp3info"
    Mp3Info.open("myfile.mp3") do |mp3info|
      puts mp3info
    end

### read/write tag1 and tag2 with Mp3Info#tag attribute

    # when reading tag2 have priority over tag1
    # when writing, each tag is written.
    Mp3Info.open("myfile.mp3") do |mp3|
      puts mp3.tag.title   
      puts mp3.tag.artist   
      puts mp3.tag.album
      puts mp3.tag.tracknum
      mp3.tag.title = "track title"
      mp3.tag.artist = "artist name"
    end

### access id3v2 tags

    Mp3Info.open("myfile.mp3") do |mp3|
      # you can access four letter v2 tags like this
      puts mp3.tag2.TIT2
      mp3.tag2.TIT2 = "new TIT2"
      # or like that
      mp3.tag2["TIT2"]
      # at this time, only COMM tag is processed after reading and before writing
      # according to ID3v2#options hash
      mp3.tag2.options[:lang] = "FRE"
      mp3.tag2.COMM = "my comment in french, correctly handled when reading and writing"
    end

    # tags v2 will be read and written according to the :encoding settings
    mp3 = Mp3Info.open("myfile.mp3", :encoding => 'utf-8')

## Requirements

* iconv

## Install

    $ ruby install.rb config
    $ ruby install.rb setup
    # ruby install.rb install

or

    gem install ruby-mp3info

## Developers

After checking out the source, run:

  $ rake newb

This task will install any missing dependencies, run the tests/specs,
and generate the RDoc.

## License

ruby

## TODO

* encoder detection
* support for more tags in id3v2
* generalize id3v2 with other audio formats (APE, MPC, OGG, etc...)
