# Final-Project-Python

## Video Demonstrating Code: https://www.youtube.com/watch?v=BjHmunom08E

#Searched up a way to get items in file into a list and found something about this on stack overflow

with open("phenotypeDmel.txt","r", encoding='utf8') as f:
    values = f.readlines()
    values = values[:200]

#https://realpython.com/python-counter/ helped with count values function 
def countValues():
    count = {}
    for phenotype in values:
        if phenotype not in count:
            count[phenotype] = 0
        count[phenotype] += 1
    return count
count = countValues()
print(count)


maxCount=0
for values in count:
    if count[values]> maxCount:
        maxCount=count[values]
    else:
        maxCount = maxCount
print(maxCount)

maxWidth = 0
widthWOspace = 0
widthWOspace = 1100/len(count)
maxWidth = widthWOspace/2

maxHeight = 0
heightWOspace = 0
heightWOspace = 500/maxCount 
maxHeight = heightWOspace/2

import turtle
turtle.setup(1200,600)

#set a backgroud

screen = turtle.Screen()
screen.title("Drosophila Gene Map")
screen.bgpic("dna.png")

t = turtle.Turtle()
t.shape("square")
t.speed(1200)
t.penup()
t.goto(0,250)
t.write("Drosophila Gene Filter Map",align="center",font=("Times New Roman",30,"bold"))

t.shapesize(maxWidth/20,maxHeight/20)
t.left(90)
t.goto(-550,-250)
   
numSquares = 0
x = 0
n = 0
for values in count:
    input = values 
    words = input.split()
    for word in words:
        if word == "female":
            t.color("magenta")
            break
        elif word == "male":
            t.color("blue")
            break
        elif word == "behavior":
            t.color("orange")
        elif word == "cell":
            t.color("green")
        else:
            t.color("black")
    n += 1
    numSquares = count[values]
    x = n*maxWidth*2
    y = maxHeight*2
    for i in range (numSquares):
        t.stamp()
        t.forward(y)
    t.goto(-550,-250)
    t.right(90)
    t.forward(x)
    t.left(90)

# learned a lot about the click function on the pythonguides.com, geeksforgeeks.com, stackoverflow.com, and techwithtim.net
z = turtle.Turtle()
z.penup()
z.shapesize(maxWidth/20)
def showValue(x, y):
    barWidth = 2 * maxWidth
    barHeight = maxHeight * 2
    barX = ((x + 550) // barWidth) * barWidth - 550
    barY = ((y + 250) // barHeight) * barHeight - 250

    index = int((barX + 550) // (2 * maxWidth))
    value = list(count.keys())[index]

    z.clear()
    z.goto(barX, barY)
    z.shape("circle")
    z.color("red")
    z.write(value + str(count[value]), align="center", font=("Arial", 12, "normal"))
    
turtle.onscreenclick(showValue)
