#把所有的目录做成变量，方便修改和移植   

#教训：不要在一个变量中定义多个路径 ，但是可以在一
#个变量中放置多个变量的值
#可以用 echo来帮助调试写的 makefile文件
T1 =./t1
T2 =./t2
T3 =./t3

# *.c文件和所有 *.o  
SRC =$(wildcard ${T1}/*.c)\
	 $(wildcard ${T2}/*.c)\
	 $(wildcard ${T3}/*.c)\
	 $(wildcard *.c)

OBJ =./obj
INC =-It1 -It2 -It3  


# *.c文件和所有 *.o  
OBJECT =$(patsubst %.c,${OBJ}/%.o,$(notdir ${SRC}))  

#可以用 echo来帮助调试写的 makefile文件
#all:
	#@echo "start debug!"
	#@echo ${SRC}
	#@echo ${OBJECT}

#设置最后目标文件  
TARGET = test  
BIN_TARGET = ${TARGET}  

CC = gcc   
CFLAGS = -g -Wall ${INC}   

#用 *.o生成可执行文件，其中可用 $^替换掉 ${OBJECT}  
${BIN_TARGET}:${OBJECT}  
	$(CC) $(CFLAGS) -o $@ ${OBJECT}  


#生成各个中间文件  
${OBJ}/%.o:${T1}/%.c   
	$(CC) -c $< -o $@ 
${OBJ}/%.o:${T2}/%.c   
	$(CC) -c $< -o $@ 
${OBJ}/%.o:${T3}/%.c   
	$(CC) -c $< -o $@ 
${OBJ}/%.o:./%.c   
	$(CC) $(CFLAGS) -c $< -o $@ 


#删除文件
.PHONY:clean  
clean:  
	#rm -rf {}命令就是删除文件 \;这是格式要求的
	#没有具体含义。
	# -exec 后面接执行命令
	find $(OBJ) -name *.o -exec rm -rf {} \; 
	rm -rf test a.out *.o 
	${MAKE} clean -C t1
	${MAKE} clean -C t2
	${MAKE} clean -C t3
