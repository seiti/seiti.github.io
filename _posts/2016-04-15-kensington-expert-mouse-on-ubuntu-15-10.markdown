---
layout: post
title: Kensington Expert Mouse on Ubuntu 15.10
date: '2016-04-15 15:13:05'
---

I recently bought a new trackball, since my *Logitech M510* stubbornly keeps sending double clicks whenever I click on it. This new trackball is the **Kensington Expert Mouse** - KEM (odd name, I figure if Kensington does sell mice named "Kensington Expert Trackball...).


![Kensington Expert Mouse/Trackball/Joystick/Whatever](http://res.cloudinary.com/dw218agtr/image/upload/v1460733546/KEM_hewrvg.jpg "Expert BigBalled")


Four buttons
-

The trackaball presents 4 buttons, a scroll whell and a very big ball right in the middle of it. The two bottom buttons are correctly mapped to right and left buttons. The top one's are the ones I dislike.

The problem is that I didn't like the *upper right* button mapped to **middle click**. I would like the **upper left** mapped to it instead.

Fortunately KEM has 4 programmable buttons. If you're using Windows/OSX and install his software, that is.

When one uses Ubuntu as OS things became a little more trickier. But not much.

Simples way to fix that is to use ``xinput`` to find out the name of the device (I wouldn't use the id, since it changes everytime):

    $ xinput                                                                                    
    ⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
    ⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
    ⎜   ↳ Logitech M570                           	id=12	[slave  pointer  (2)]
    ⎜   ↳ Kensington      Kensington Expert Mouse 	id=13	[slave  pointer  (2)]
    ⎜   ↳ Broadcom Corp. Bluetooth USB Host Controller	id=15	[slave  pointer  (2)]
    ⎜   ↳ bcm5974                                 	id=17	[slave  pointer  (2)]
    ⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]


Then simply input: 

    xinput set-button-map "Kensington      Kensington Expert Mouse" 1 2 3 4 5 6 7 2

The last `2` means _middle click_, and it's position on the list represents the _upper left button_. I'm kepping the upper right button as is, since I don't use it.

Persisting
=

Simply add the aforementioned command to **startup applications**. And that's it.