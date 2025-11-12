# gamesnake
import turtle
import random
import time

delay = 0.15
score = 0
high_score = 0

# สร้างหน้าจอเกม
wn = turtle.Screen()
wn.title("🐍 Cute Snake Game 💖")
wn.bgcolor("#FFF8E7")
wn.setup(width=700, height=700)
wn.tracer(0)

# วาดกรอบ
border = turtle.Turtle()
border.speed(5)
border.pensize(4)
border.penup()
border.goto(-310, 250)
border.pendown()
border.color("#FFD6E0")
for _ in range(2):
    border.forward(600)
    border.right(90)
    border.forward(500)
    border.right(90)
border.hideturtle()

# สร้างหัวงู
head = turtle.Turtle()
head.speed(0)
head.shape("circle")
head.color("#6EE7B7")  # เขียวมิ้นต์
head.penup()
head.goto(0, 0)
head.direction = "stop"

# ตางู
eye_left = turtle.Turtle()
eye_left.shape("circle")
eye_left.color("white")
eye_left.penup()
eye_left.goto(head.xcor() - 6, head.ycor() + 6)

eye_right = turtle.Turtle()
eye_right.shape("circle")
eye_right.color("white")
eye_right.penup()
eye_right.goto(head.xcor() + 6, head.ycor() + 6)

# อาหารงู
food = turtle.Turtle()
food_color = random.choice(['#F9A8D4', '#FDE68A', '#93C5FD', '#A7F3D0'])
food_shape = random.choice(['triangle', 'circle', 'square'])
food.speed(0)
food.shape(food_shape)
food.color(food_color)
food.penup()
food.goto(20, 20)

# สกอร์บอร์ด
scoreBoard = turtle.Turtle()
scoreBoard.speed(0)
scoreBoard.shape("square")
scoreBoard.color("#F472B6")
scoreBoard.penup()
scoreBoard.hideturtle()
scoreBoard.goto(0, 250)
scoreBoard.write("Score : 0   High Score : 0", align="center", font=("Comic Sans MS", 24, "bold"))

# ฟังก์ชันควบคุมการเคลื่อนที่
def move_up():
    if head.direction != "down":
        head.direction = "up"
def move_down():
    if head.direction != "up":
        head.direction = "down"
def move_left():
    if head.direction != "right":
        head.direction = "left"
def move_right():
    if head.direction != "left":
        head.direction = "right"

def move():
    if head.direction == "up":
        y = head.ycor()
        head.sety(y + 20)
    if head.direction == "down":
        y = head.ycor()
        head.sety(y - 20)
    if head.direction == "left":
        x = head.xcor()
        head.setx(x - 20)
    if head.direction == "right":
        x = head.xcor()
        head.setx(x + 20)
    
    # อัปเดตตำแหน่งตาให้อยู่ตามหัว
    eye_left.goto(head.xcor() - 6, head.ycor() + 6)
    eye_right.goto(head.xcor() + 6, head.ycor() + 6)

# การควบคุมด้วยแป้นพิมพ์
wn.listen()
wn.onkeypress(move_up, "Up")
wn.onkeypress(move_down, "Down")
wn.onkeypress(move_left, "Left")
wn.onkeypress(move_right, "Right")

segments = []

# สีลำตัวพาสเทล
body_colors = ["#F9A8D4", "#FDE68A", "#93C5FD", "#A7F3D0", "#C4B5FD"]

# ลูปหลักของเกม
while True:
    wn.update()

    # ชนขอบ
    if head.xcor() > 280 or head.xcor() < -300 or head.ycor() > 240 or head.ycor() < -240:
        time.sleep(1)
        head.goto(0, 0)
        head.direction = "stop"
        for segment in segments:
            segment.goto(1000, 1000)
        segments.clear()
        score = 0
        scoreBoard.clear()
        scoreBoard.write("Score : {}   High Score : {}".format(score, high_score), align="center", font=("Comic Sans MS", 24, "bold"))

    # ชนอาหาร
    if head.distance(food) < 20:
        score += 10
        if score > high_score:
            high_score = score

        scoreBoard.clear()
        scoreBoard.write("Score : {}   High Score : {}".format(score, high_score), align="center", font=("Comic Sans MS", 24, "bold"))

        # เอฟเฟกต์ประกาย ✨
        for _ in range(2):
            head.color("#FDE68A")
            wn.update()
            time.sleep(0.1)
            head.color("#6EE7B7")
            wn.update()
            time.sleep(0.1)

        # ย้ายอาหาร
        x_cord = random.randint(-14, 13) * 20
        y_cord = random.randint(-11, 11) * 20
        food_color = random.choice(body_colors)
        food_shape = random.choice(['triangle', 'circle', 'square'])
        food.shape(food_shape)
        food.color(food_color)
        food.goto(x_cord, y_cord)

        # เพิ่มลำตัว
        new_segment = turtle.Turtle()
        new_segment.speed(0)
        new_segment.shape("circle")
        new_segment.color(random.choice(body_colors))
        new_segment.penup()
        segments.append(new_segment)

    # เคลื่อนลำตัวตามหัว
    for i in range(len(segments) - 1, 0, -1):
        x = segments[i - 1].xcor()
        y = segments[i - 1].ycor()
        segments[i].goto(x, y)
    if len(segments) > 0:
        segments[0].goto(head.xcor(), head.ycor())

    move()

    # ชนตัวเอง
    for segment in segments:
        if segment.distance(head) < 20:
            time.sleep(1)
            head.goto(0, 0)
            head.direction = "stop"
            for segment in segments:
                segment.goto(1000, 1000)
            segments.clear()
            score = 0
            scoreBoard.clear()
            scoreBoard.write("Score : {}   High Score : {}".format(score, high_score), align="center", font=("Comic Sans MS", 24, "bold"))

    time.sleep(delay)
