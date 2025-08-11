# Fake Compositor
An X based application which emulates a compositor and 2 apps, each export either RGB or YUV buffers in encrypted or non-encrypted format. Compositor exports these buffers onto dma-buf and display them on the screen. TMZ buffers will have a RED color border and non-TMZ buffers contains Green Color border. It works with TMZ enabled HW only.

App1 and App2 buffers are static buffers and can be of type TMZ or non-TMZ. These 2 buffers need to be blend on to the composited buffer(dma-buf). Based on the type of the compositor buffer, the final picture will be displayed.

<img width="1007" height="324" alt="image" src="https://github.com/user-attachments/assets/466ffe52-4f3f-4e1e-802c-9b733c862b4a" />

Fake compositor operates in 3 modes.
1. notmz
2. app
3. both

Case 1 : When run in “notmz” mode, TMZ isn't used at all. Meaning, neither apps nor compositor uses TMZ. In this case, the application surface borders will display in Green Color. Compositor can blend these Apps buffers and can display it. Here is the sample output for the same. 

<img width="417" height="329" alt="image" src="https://github.com/user-attachments/assets/09c94d5c-dc47-48fa-a40b-abdc9f555cfa" />


Case 2 : When run in “app” mode, App1 will generate non-TMZ buffers,  App2 generates TMZ buffers and compositor is non-TMZ buffers. As the compositor buffers is non-tmz, it can’t blend App1’s non-TMZ and App2’s TMZ buffers. Here is the Sample output for the same. 

<img width="409" height="357" alt="image" src="https://github.com/user-attachments/assets/1bee53e1-6f17-4d7f-bd11-787124c3653e" />


Case 3 : When run in “both” mode, App1 will generate non-TMZ buffers,  App2 generates TMZ buffers (RED Border) and compositor generates TMZ buffers. As the compositor buffers is TMZ, it will blend App1’s non-TMZ and App2’s TMZ buffers. Here is the Sample output for the same. 

<img width="412" height="340" alt="image" src="https://github.com/user-attachments/assets/5cf4d4f4-9273-426f-8dfc-bce3056b8a60" />


# Compile :
   gcc fake_compositor.c -g -lEGL -lGL -lX11 -lm -lgbm -ldrm -I/usr/include/libdrm -o fake_compositor

   
./fake_compositor  <tmz_mode>   => <tmz_mode> needs to be any one of notmz, app or both.
