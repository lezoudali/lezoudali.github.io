---
layout: post
title:  Simple Cryptography Progam in C
date:   2015-01-26 19:20:00
categories: jekyll update
---

For my first (real) post, I’ve decided to share one of the first, somewhat useful, programs I wrote when I started learning C. It’s a simple text encryption program called [Vigenère cypher][vigenere]. This program uses a cypher algorithm to encrypt a text by using a keyword. The Vigenère cypher is a more secure version of the [Caesar cypher][caesar], which uses a single character or an integer for a key. How exactly does the  Vigenère cypher work you ask? Well, Let’s say you want to communicate with your crush  via text messages and you really don’t want anyone else to know what you are talking about. You might want to use the Vigenère cipher with a keyword, which only you and crush know, to encrypt your messages. For example, using the keyword __belle__ (beautiful in french), the message __Wanna have lunch tomorrow?__ encrypts to __Xeyye iegp pvrns xpqzcvpa?__. The letter ‘b’ in the keyword corresponds to a shift of 1, ‘e’ corresponds to a shift of 4 and ‘l’ corresponds to a shift of 11. When writing this program, you must keep in mind that the alphabet and keyword act as wheel that wraps around itself when the last letter of the keyword or alphabet is reached.  We do not encrypt spaces or non alphabetical characters. see below...

{% highlight c %}
#define MAX 200
#include <stdio.h>
#include <ctype.h>
#include <string.h>
 
int main(void){
    char message[MAX];
    char keyword[MAX]; 
    int key_id, ascii_val;
    char key, character, letter;

    printf("message (< 140 chars): ");
    fgets(message, MAX, stdin);
    
    printf("keyword: ");
    scanf("%s", keyword);

    int key_length = strlen(keyword);

    printf("\nEncrypted text: ");

    for (int i = 0, n = strlen(message); i < n; ++i){
        character = message[i];
        key = keyword[key_id];
        key = islower(key) ? key - 97 : key - 65;
         
        if (isalpha(character)) {
           ascii_val = islower(character) ? 97 : 65;
           letter = (((character - ascii_val) + key) % 26) + ascii_val;
           key_id = (key_id + 1) % key_length;
           printf("%c", letter);
        }
        else
           printf("%c", character);
    }
    printf("\n");
    return 0;
}
{% endhighlight %}

###OUTPUT

{% highlight c %}
message (< 140 chars): wanna have lunch tomorrow
keyword: belle

Encrypted text: xeyye iegp pvrns xpqzcvpa
{% endhighlight %}

[vigenere]: http://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher
[caesar]: http://en.wikipedia.org/wiki/Caesar_cipher