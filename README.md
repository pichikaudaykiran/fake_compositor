# fake_compositor
An X based application which emulates a compositor and 2 apps, each export either RGB or YUV buffers in encrypted or non-encrypted format. Compositor exports these buffers onto dma-buf and display them on the screen. TMZ buffers will have a RED color border and non-TMZ buffers contains Green Color border. It works with TMZ enabled HW only.
