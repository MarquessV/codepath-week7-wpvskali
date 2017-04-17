# Project 7 - WordPress Pentesting

Time spent: **3** hours spent in total

> Objective: Find, analyze, recreate, and document **three vulnerabilities** affecting an old version of WordPress

## Pentesting Report

	
1. (Required) Authenticated Stored Cross-Site Scripting via Image Filename (ID: 8615)

  - [x] Summary: 
    - Vulnerability types: XSS
    - Tested in version: 4.0.1
    - Fixed in version: 4.6.1
    
    I uploaded an image with the file name NormalLookingImageName<img src=a onerror=alert('imagexss')>.jpg and included it in a post. Image filenames aren't sanitized, so the code executes whenever someone loads the page.
    
  - [x] GIF Walkthrough: 
		<img src='http://i.imgur.com/GelORed.gif' title='Exploit 1' width='' alt='Exploit 1' />
  - [x] Steps to recreate:
		1. Upload an image with XSS code in the filename and put it in a post.
		Ex: NormalLookingImageName<img src=a onerror=alert('imagexss')>.jpg
  - [x] Affected source code:
    - [Link 1](https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0)

2. (Required) Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds (ID: 8768)
  - [x] Summary: 
    - Vulnerability types: XSS
    - Tested in version: 4.0.1
    - Fixed in version: 4.7.2
    
	I referred to the linked blog post on the vulnerability page to recreate the exploit. It works by taking advantage of an oversight in the regex that is supposed to sanitize the embed code. It was fixed in future versions of wordpress by using the urlencode() function.
	
  - [x] GIF Walkthrough: 
		<img src='http://i.imgur.com/AXnl9jA.gif' title='Exploit 2' width='' alt='Exploit 2' />  
  - [x] Steps to recreate: 
		1. Create a new post with embed code specifically crafted to bypass sanitization.
			Ex: [embed src='https://youtube.com/embed/12345\<svg onload=alert(1)>'][/embed]
  - [x] Affected source code:
    - [Link 1](https://github.com/WordPress/WordPress/commit/419c8d97ce8df7d5004ee0b566bc5e095f0a6ca8)

3. (Required) Authenticated Stored Cross-Site Scripting (XSS) (ID: 8111)
  - [x] Summary: 
    - Vulnerability types: XSS
    - Tested in version: 4.0.1
    - Fixed in version: 4.2.4
    
	I referred to the linked blog post on the vulnerability to recreate the exploit. By putting code in the title tag of an html link input sanitization is avoided.
	
  - [x] GIF Walkthrough:
		<img src='http://i.imgur.com/lki7Yhh.gif' title='Exploit 3' width='' alt='Exploit 3' />  
  - [x] Steps to recreate: 
		1. Create a new post, insert your code in the title tag of a link.
			Ex: <a href="[caption code=">]</a><a title=" onmouseover=alert('test')  ">link</a>
  - [x] Affected source code:
    - N/A

## Assets

N/A

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Setting up wordpress using Docker and eventually Vagrant on Windows was much harder than anything else.

## License

    Copyright [2017] [Marquess Valdez]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
