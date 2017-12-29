Test1 = "Two roads [__1__] in a yellow wood, And sorry I could not travel both And be one [__2__], long I stood And looked down one as far as I could To where it [__3__] in the [__4__]."
Test2 = "The silver swan, who living had no note,  When death [__1__], unlocked her silent [__2__]; Leaning her [__3__] against the reedy shore, Thus sung her first and last, and [__4__] no more: Farewell, all joys; O death, come close mine eyes; More geese than [__5__] now live, more fools than wise."
Test3 = "How [__1__] is the winning of a kiss at loves beginning, When two [__2__] hearts are sighing For the knot there's no [__3__]. Yet remember, mist your wooing, Love is [__4__], but love has ruining; Other smiles may make you [__5__], Tears for charm may [__6__]. "
answer1 = ["diverged","traveler","bent","undergrowth"]
answer2 = ["approached","throat","breast","sung","swans"]
answer3 = ["delicious","mutual","untying","bliss","fickle","tickle"]
space = []
n = 1
while n<7:
    space.append("[__"+str(n)+"__]")
    n += 1

def word_in_test(word, space_of_test):#用于判断要替换的空格,输入是一单词和一个列表。输出是要替换的单词或者无输出
    for parts in space_of_test:
        if parts in word:
            return parts
    return None   

def replaced():#用来最后执行的函数，输出是正确的答案。
    test = select()
    if test != False:
        print(test)
        answer =Answer(test)
        test_list = test.split()
        n=0#n和count都是用来结束循环的，不过n是用来结束整个循环，而count是用来输错两次后结束循环
        count = 0
        for part in test_list:
            if  word_in_test(part,space) != None:
                while n < len(answer):
                    if count ==0:
                        if guess(answer[n])== True:
                            test=test.replace(space[n],answer[n])
                            n+= 1
                            print(test)
                        else:
                            count += 1  
                    else:
                        break

import random#引入随机数
def select():#进入的界面，玩家输入想要进行的难度或随机难度，输出对应的文档
    n = input("Welcome to the Python Challager!\nPlease choose your quiz level:\n0 - easy\n1 - medium\n2 - hard\n3 - advanced\n")
    if n == "0":
        return Test1
    if n == "1":
        return Test2
    if n == "2":
        return Test3
    if n == "3":
        return [Test1,Test2,Test3][random.randint(0,2)]
    else:
        return False

def guess(answer):#验证猜测的和答案是否一致，输入答案和玩家输入的内容，输出是否和答案一致
    gss = input("Please input you answer in the first one blank\n")
    count = 0
    if gss ==answer:
        return True
    while gss !=answer:
        if count == 0:
            gss = input("Try again\n")
            count +=1
        else:
            print("game over")
            break

def Answer(test):#用来找到题目对应的答案，输入是文件，输出是文件对应的答案
    if test == Test1:
        return answer1
    if test == Test2:
        return answer2
    if test == Test3:
        return answer3

replaced()
