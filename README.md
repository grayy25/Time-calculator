
# Time Calculator

This is the boilerplate for the Time Calculator project. Instructions for building your project can be found at https://www.freecodecamp.org/learn/scientific-computing-with-python/scientific-computing-with-python-projects/time-calculator


import math


def add_time(start, duration, *args):

  stlst = start.split()
  med = start[-2:]

  st = stlst[0].split(":")
  dr = duration.split(":")

  hr1 = st[0]
  hr2 = dr[0]
  min1 = st[-1][0:2]
  min2 = dr[-1]

  if(hr2==0 and min2==0):
    return start

  min = int(min1) + int(min2)
  hr = int(hr1) + int(hr2)
  while (min > 60):
    hr += 1
    min -= 60

  #result_1 = str(num).zfill(5)
  #print("hour is:", hr)
  min = str(min).zfill(2)
  #print(hr)
  flip = 0
  rem = 0
  
  if(hr==12):
    flip=1
    rem=1
    
  if (hr >12):
    flip = hr // 12
    if(med=="PM"):
  
      rem = math.ceil(hr / 24)
    else:
      rem=math.floor(hr/24)

    for i in range(flip):
      hr -= 12

    



  
  if (flip % 2 != 0):
    if (med == "AM"):
      med = "PM"
      if (rem == 1):
        rem = 0
    else:
      med = "AM"

  noDays = " "
  #time=" "
  if (rem == 0):
    noDays = " "
  elif (rem == 1):
    noDays = "(next day)"
  else:
    noDays = str(rem) + " " + "days later"
    noDays = f"({noDays})"

    #print(noDays)
  if(hr==0):
    hr=12
  if (len(noDays) > 3):
    new_time = str(hr) + ":" + min + " " + str(med) + " " + noDays
  else:
    new_time = str(hr) + ":" + min + " " + str(med)
    
  #new_time = "\"%s\"" % time
  daysLst = {
    "Monday": 0,
    "Tuesday": 1,
    "Wednesday": 2,
    "Thursday": 3,
    "Friday": 4,
    "Saturday": 5,
    "Sunday": 6
  }

  if (args):
    val = 0
    currday=" "
    for i in daysLst:
      if (args[0].title() == i):
        currday=args[0].title()
        val = daysLst[i] + rem

    if (val > 6):
      val = val % 7
    k = list(daysLst.keys())
    v = list(daysLst.values())

    pos = v.index(val)
    day = k[pos]
    if(day==currday):
      new_time = str(hr) + ":" + min + " " + str(med) + "," + " " + str(
      day)
    else:
        new_time = str(hr) + ":" + min + " " + str(med) + "," + " " + str(
      day) + " " + noDays
    #new_time = "\"%s\"" % time

  return new_time


print(add_time("2:59 AM", "24:00"))
