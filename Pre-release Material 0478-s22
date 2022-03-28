#0478_S22_PM

#导入时间模块
import time

############### TASK 1 ###############
#Show the days available for booking (Task 1.3)
def displayValidDays(now):  #参数now为本地当前时间，参数类型为time
    #time类型的时间是以秒为单位的浮点小数时间戳，表示距1970年1月1日0点已经过了多少秒
    secsInADay = 24 * 60 * 60           #每天的秒数
    secsInAWeek = 7 * secsInADay        #每周的秒数
    validDayStart = now + secsInAWeek   #可预订的起始日期：从现在起的一周后
    validDays = []                      #可预订的所有日期：初始化为空列表

    #显示部分：
    # 1.使用time模块的 strftime 方法将以秒数表示的时间格式化，语法：time.strftime(<format string>, <time tuple>)
    #   参数 <format string> 是格式控制字符串，其中
    #       %B 使用完整的月份名称
    #       %Y 使用四位数年份表示
    #       %A 使用完整星期名称
    #   参数 <time tuple> 是时间元组
    #       时间元组包括九组数字：四位数年、月、日、小时、分钟、秒、一周的第几日、一年的第几日、夏令时     
    # 2. 使用time模块的 localtime 方法来将时间戳转换为本地时间下的时间元组，以得到strftime的第二个参数
    print("\nToday is", time.strftime("%B %d,%Y(%A)", time.localtime(now)))
    print("The days available for booking:")
    for i in range(0, 7):
        day = validDayStart + secsInADay * i    #下一周每天的时间戳
        print(i+1, "-", time.strftime("%b. %d,%Y(%a)", time.localtime(day)))
        validDays.append(day)   #将计算出来的时间戳加入到validDays列表中
    print() #打印空行
    return validDays

#Display the options, attractions and prices for one-day or two-day tickets (Task 1.1 & 1.2)
#这里设计了一个单独的displayTickets函数，用来实现显示不同类型票的属性的功能。
#这样设计的目的是将数据和方法分离，方便后期对数据进行修改。
#更好的方法是使用类实现。
#   参数ticketType的类型为int，代表 one-day 或 two-day
#   参数ticketList的类型是列表，用于从函数外输入数据，数据设计为二元列表（故每个元素需要用两个下标表示），具体见第 行定义的list数据
def displayTickets(ticketType, ticketList):
    #使用格式化输出来根据不同的ticketType输出不同的表头，%s代表当前位置的数据为字符串，%(<data>)中的内容是%s位置要显示的数据
    #使用条件表达式简化选择结构，语法：a if p else b，意义为如果p为真就返回a否则返回b
    print("********** %s-day Tickets **********" % ("One" if ticketType == 1 else "Two"))
    #根据设计的数据结构显示对应的表格
    for i in range(5):  #五种基本票
        print(i+1, "-", "%s \t\t costs \t $%.2f %s" % (ticketList[0][i], ticketList[ticketType][i], ticketList[3][i]))
    print("# Extra Attractions:")
    for i in range(2 if ticketType == 1 else 3):    #两种或三种扩展票
        print(i+1, "-", "%s \t costs \t $%.2f per person" % (ticketList[4][i], ticketList[5][i]))
    print(); #显示空行

#显示提示和报错
def displayIntroductions():
    print("********** Introdutions **********")
    warning1()
    warning2()
    
def warning1():
    print("# An adult may bring up to two children.")

def warning2():
    print("# Family ticket includes up to two adults or seniors, and three children.")


############### TASK 2 ###############
#为了实现输入有效数据的功能，使用了条件中断结构：
# while True:
#     <statements>
#     if <condition>:
#         break
#     else:
#         <statements>  

#选择订票日期
def choosingDate():
    while True:
        result = (int)(input("### Please input the number of the date in the list(1~7): "))
        if result in range(1, 8):
            break
        else:
            print("Invalid Value!")
    return result

#订票流程
def bookingTickets():
    print("********************BOOKING TICKET*********************")
    date = choosingDate() - 1 #将显示的列表序号转换为对应列表下标

    #选择订票类型(Task 2.1)
    while True:
        ticketType = (int)(input("### Please choose the type of tickets\n(input 1 for One-Day Tickets, 2 for Two-Day Tickets): "))
        if ticketType in range(1, 3):
            break
        else:
            print("Invalid Value!")

    #输入成人人数
    adults = (int)(input("Please input the number of Adults in your team: "))
    
    #输入儿童人数
    while True:
        children = (int)(input("Please input the number of Children in your team(up to %d): " % (adults * 2))) #一个成人可以带两个儿童（显示最多儿童人数）
        if(children <= adults * 2):
            break
        else:
            print("Invalid Value!")
            warning1()

    #输入老人人数        
    seniors = (int)(input("Please input the number of Seniors in your team: "))
    
    #计算总人数
    total = adults + children + seniors
    
    #选择要购买的扩展票
    print("Please choose Extra Attractions:")
    lionFeeding = total if input("Do you want to choose Lion Feeding Attraction? (Y/N): ") == 'Y' else 0    #Lion Feeding 的票数
    penguinFeeding = total if input("Do you want to choose Penguin Feeding Attraction? (Y/N): ") == 'Y' else 0  #Penguin Feeding 的票数
    if ticketType == 2:  #如果选择两日票
        eveningBBQ = total if input("Do you want to choose Evening Barbecue Attraction? (Y/N): ") == 'Y' else 0 #BBQ 的票数
    else:
        eveningBBQ = 0
    
    result = [ticketType, adults, children, seniors, total, lionFeeding, penguinFeeding, eveningBBQ, date]  #将各数据整理成列表返回
    return result

#计算总价(Task 2.1)
#同样使用了数据和功能分离的方法，通过参数传入订单数据和票价数据
def calculatingCosts(order, ticketList):
    costWithoutExtra = 0    #基本票的总价
    for i in range(0, 3):   #基本票的总价 = 成人人数×成人票价 + 儿童人数×儿童票价 + 老人人数×老人票价
        costWithoutExtra += order[i+1] * ticketList[order[0]][i]
        #order[0]为ticketType，order[2]~order[3]分别是成人、儿童、老人的人数

    costExtra = 0           #扩展票的总价
    for i in range(0, 3):   #扩展票的总价 = 狮子票数×狮子票价 + 企鹅票数×企鹅票价 + BBQ票数×BBQ票价
        costExtra += order[i+5] * ticketList[5][i]
        #order[4]~order[6]分别是狮子、企鹅、BBQ的票数
    result = [costWithoutExtra, costExtra, costWithoutExtra+costExtra] #将两种价格及总价整理成列表返回
    return result

############### TASK 3 ###############
#最优订票方案(Task 3)
#思路：
# 1.优惠主要体现在Family Ticket和Team Ticket中，所以无需考虑扩展票，只考虑基本票价是否存在优惠
# 2.若人数大于等于六人，计算对应类型的TeamTicket总价，并与原总价进行对比
# 3.若人数小于六人，并符合FamilyTicket的人员条件，将对应类型的FamilyTicket与原总价进行对比
def ensuringBestValue(order, ticketList):
    print("The total cost is $%d." % calculatingCosts(order, ticketList)[2]) #显示总价
    costs = calculatingCosts(order, ticketList)[0]  #原总价（不含扩展票）
    change = False  #设置逻辑变量，用来存储是否变更订票方案
    #如果人数大于等于6，讨论TeamTicket方案是否优惠
    if order[4] >= 6:
        temp = order[4] * ticketList[order[0]][3]
        if temp < costs:
            change = True if input("You can choose Team Ticket to save $%d! Change Ticket?(Y/N): " % (costs - temp)) == 'Y' else False
    #如果人数小于6，讨论FamilyTicket方案是否优惠
    elif order[1]+order[3]<=2 and order[2] <= 3:    #up to two adults or seniors, and three children
        temp = ticketList[order[0]][4]
        if temp < costs:
            change = True if input("You can choose Family Ticket to save $%d! Change Ticket?(Y/N): " % (costs - temp)) == 'Y' else False

    #最终支付金额取决于change是否为真
    result = temp + calculatingCosts(order, ticketList)[1] if change else calculatingCosts(order, ticketList)[2]
    print("You need to pay $%d, thank you." % result)


############### DATA LISTS ###############
ticketTypeList = ["Adult", "Child", "Senior", "Team", "Family"]
oneDayTicketList = [20.0, 12.0, 16.0, 15.0, 60.0]
twoDayTicketList = [30.0, 18.0, 24.0, 22.5, 90.0]
unitList = ["per person", "per person", "per person", "per person", "in total"]
extraAttractionTypeList = ["Lion Feeding", "Penguin Feeding", "Evening BBQ"]
extraAttractionList = [2.5, 2.0, 5.0]
ticketList = [ticketTypeList, oneDayTicketList, twoDayTicketList, unitList, extraAttractionTypeList, extraAttractionList]

############### MAIN ###############
print("\n##### WELCOME TO WILDLIFE PARK! #####")
displayTickets(1, ticketList)   #task 1.1
displayTickets(2, ticketList)   #task 1.2
displayIntroductions()          #task 1
now = time.time()               #获取当前时间戳
dates = displayValidDays(now)   #将下一周七天的时间戳存储在dates列表中

while True:
    booking = bookingTickets()  #执行订票流程，将数据存储在booking列表中 task 2.1
    ensuringBestValue(booking, ticketList)  #计算优惠方案 task 3
    
    #Task 2.3 分配一个独立的预定号码，这里使用的是预定的时间戳
    #也可以使用一些加密算法
    numOfDate = booking[8]  #根据订单确定预定的日期（第几天）
    print("Your Ticket Serial Number is %d." % ((int)(dates[numOfDate]))) #显示预定日期的时间戳
    print("########## Have A Nice Day! ##########\n\n\n\n\n")
