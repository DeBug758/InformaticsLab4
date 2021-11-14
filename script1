file = open("input.json", "r")
A = file.read()
file.close()

file = open("output.xml", "w")
file.write("<?xml version=\"1.0\" encoding=\"UTF-8\" ?>")

begin = True
opened = False
L = list()
mass = list()
record = True
array = list()
array.append('')
flag = False
for i in A:
    if i != '{' and i != '}' and i != '[' and i != ']' and i != '\"' and i != ',' and i != ':' and i != '\n':
        if begin is False and record is True:
            mass.append(i)
        file.write(i)
    elif i == '\"':
        if record:
            if begin:
                begin = False
                file.write('<')
            else:
                begin = True
                file.write('>')
                L.append(''.join(mass))
                mass.clear()
    elif i == ':':
        record = False
    elif i == ',' and record is False:
        record = True
        file.write('</' + L[-1] + '>')
        L.pop(-1)
    elif i == '}':
        if opened:
            file.write('</' + array[-1] + '>')
        elif record and len(L) > 0:
            file.write('</' + L[-1] + '>')
            L.pop(-1)
    elif i == '[':
        record = True
        array.append(L[-1])
        L.pop(-1)
        opened = True
    elif i == ']':
        opened = False
    elif i == '\n':
        if record is False:
            file.write('</' + L[-1] + '>\n')
            L.pop(-1)
            record = True
        else:
            file.write('\n')
    elif i == '{':
        record = True
        if opened and len(array) == 2:
            if flag:
                file.write('<' + array[-1] + '>')
            else:
                flag = True
file.close()
