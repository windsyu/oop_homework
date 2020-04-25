# Homework4 Personal Dairy


## ��Ŀ���� Description

The Personal Diary is a CLI (Command Line Interface) software, consists of three programs:

```
pdadd 
pdlist [ ]
pdshow 
pdremove 
```

pdadd is used to add an entity into the diary for the date. If an entity of the same date is in the diary, the existing one will be replaced. pdadd reads lines of the diary from the stdin, line by line, until a line with single '.' character or the EOF character (Ctrl-D in Unix and Ctrl- Z in Windows).

pdlist lists all entities in the diary ordered by date. If start and end date are provided through command line parameters, it lists entities between start and end only. This program lists to the stdout.

pdshow prints the content of the entity specified by the date to the stdout. 

pdremove removes one entity of the date. It returns 0 at success and -1 at failure.

The software stores diary in one data file, reads to the memory at begining of each program and stores back to the file at the end of process.

Common classes and functions should be shared between programs. No interactive is permitted, so these programs are able to work together by the means of redirection or tee, are able to be used in a shell script.

====

## ���˵�� Class Description

Diary.h �ṩDiary����࣬�������½ӿڣ�

```
static int today(); //���ؽ�������ڣ���������int����20161210

Dairy(string filename); //���캯������Ҫ����һ���洢���ļ�������"data.txt"���ļ����Բ�����

virtual ~Dairy(); //����������������д�뵽ͬһ���ļ�

void pdadd(int date,string& content); //�����������ռ����ݣ����ڴ��д洢֮

void pdlist(int begin=0,int end=99999999,bool friendly=true); //��ʾ��begin��end֮�����е��ռǣ��������friendly=False���պ��ļ��洢��ʽͬ������ʽ��������������޷�д���ļ�ʱ�����������Է�ֹ���ݶ�ʧ��

string pdshow(int date=today());//��ʾ�������ڵ��ռ�

int pdremove(int date);//ɾ���������ڵ��ռ�
```

ʹ����������4��cpp�ļ������������ļ򵥵���������û�����

====

# ���Դ��� Test

```bash
make clean
make

cp data.txt data.txt.bak
./pdlist
./pdlist 20161201 20161231

echo """I can accept content from pipe!
these programs are able to work together by the means of redirection or tee!
""">tmp.txt
./pdadd<tmp.txt
./pdshow
rm tmp.txt

./pdremove 20160101
./pdshow 20160101
echo $? #this will output 255, which means -1 is returned by the program

rm data.txt
mv data.txt.bak data.txt
```

Here is the screenshot of these test code:

![1](screen1.jpg)

![2](screen2.jpg)