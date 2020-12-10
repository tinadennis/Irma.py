# Irma.py

import turtle


def irma_setup():
    """Creates the Turtle and the Screen with the map background
       and coordinate system set to match latitude and longitude.

       :return: a tuple containing the Turtle and the Screen

       DO NOT CHANGE THE CODE IN THIS FUNCTION!
    """
    import tkinter
    turtle.setup(965, 600)  # set size of window to size of map

    wn = turtle.Screen()
    wn.title("Hurricane Irma")

    # kludge to get the map shown as a background image,
    # since wn.bgpic does not allow you to position the image
    canvas = wn.getcanvas()
    turtle.setworldcoordinates(-90, 0, -17.66, 45)  # set the coordinate system to match lat/long

    map_bg_img = tkinter.PhotoImage(file="images/atlantic-basin.png")

    # additional kludge for positioning the background image
    # when setworldcoordinates is used
    canvas.create_image(-1175, -580, anchor=tkinter.NW, image=map_bg_img)

    t = turtle.Turtle()
    wn.register_shape("images/hurricane.gif")
    t.shape("images/hurricane.gif")

    return (t, wn, map_bg_img)


def irma():
    """Animates the path of hurricane Irma
    """
    (t, wn, map_bg_img) = irma_setup()

    # your code to animate Irma here

    t.speed(0)
    file = open("data/irma.csv", "r")
    data = file.readlines()

    t.penup()
    t.goto(float(data[1].split(",")[3]), float(data[1].split(",")[2]))
    t.pendown()

    for line in data:
        line = line.split(",")

        if line[0] =="Date":
            continue
        t.goto(float(line[3]), float(line[2]))

        if float(line[4]) >= 157:
            t.width(10)
            t.color("red")
            t.write('5')
        elif float(line[4]) >= 130:
            t.width(8)
            t.color("orange")
            t.write('4')
        elif float(line[4]) >= 111:
            t.width(6)
            t.color("yellow")
            t.write('4')
        elif float(line[4]) >= 96:
            t.width(4)
            t.color("green")
            t.write('4')
        elif float(line[4]) >= 74:
            t.width(1)
            t.color("blue")
            t.write('4')
        else: 
            t.width(1)
            t.color("white")


    turtle.done()
             

if __name__ == "__main__":
    irma()
