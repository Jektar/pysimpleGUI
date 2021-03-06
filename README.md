# pysimpleGUI
A library to make setting up GUI's in pygame more manageable and simple. This is based on the pygame library

To use this module, you will need to have pygame installed in your interpreter. Since this library is not (yet) in any pip files, you will need to download the main code and place it in the folder of the program you want to use. 
Then, you can import and use it like a normal library.

Example code:

    from pysimpleGUI import *
    from pygame.locals import *

    import sys

    def myFunc(_):
        print('This is a dummy function!')

    WS = pg.display.set_mode((640, 480))

    layouts = [Layout()]

    rect = GUIRect((200, 100), (150, 75), RED)
    layouts[0].addButton(Button(rect, myFunc, textBox=TextBox((200, 100), BLACK, 'This a dummy button', font=tinyFont)))

    currentLayout = 0 #Uses a variable to controll what layout is currently used

    [layout.setSurface(WS) for layout in layouts] #Updates the surface on all layouts


    while True:
    #Main loop
        for event in pg.event.get():
            if event.type == QUIT:
                pg.quit()
                sys.exit()

            if event.type == MOUSEBUTTONDOWN:
                x, y = pg.mouse.get_pos()
                layouts[currentLayout].collide((x, y)) #Cailling the update function uppon user pressing the mouse

        WS.fill(WHITE)
        layouts[currentLayout].draw() #Draws every object every frame
        pg.display.update()


What objects exist in this library?

The main object in pysimpleGUI is the layout object. This starts as a black surface, you can add elements to. The surface object contains methods for displaying everything contained in it as well as a collision method for when the user has clicked a spot:

Layout contains:

Layout.draw() method, displays the layout, has to be called every frame

Layout.collide(point) method (point is an iterable of length 2), checks collisions

Layout.addBar(bar) method (bar is a slider or bar object), adds a bar or slider object to the layout

Layout.addButton(button) method, add a button object to the layout

Layout.addTextBox(textBox) method, adds a tex box to the layout

Layout.addShape(shape) method, adds a shape object (either GUIRect or GUICircle)

Layout.addSelector(selector) method, adds a selector object to the layout

Layout.setSurface(surface) method, used to set the pygame surface object that all elements of the layout blit to

Layout.checksurface() method, returns True if all surfaces in the layout have been set

Layout.buttons   ; list of all buttons

Layout.bars      ; list of all bars (and selectors)

Layout.textBoxes ; list of all texBoxes

Layout.shapes    ; list of all shape objects (GUIRect and GUICircle)

Layout.selectors ; list of all selectors objects

TextBox contains:
