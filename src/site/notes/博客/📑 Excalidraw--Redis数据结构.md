---
{"excalidraw-plugin":"parsed","tags":["excalidraw"],"dg-path":"Excalidraw/📑 Excalidraw--Redis数据结构","dg-publish":true,"permalink":"/Excalidraw/📑 Excalidraw--Redis数据结构/","dgPassFrontmatter":true}
---

==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
dict
{ #bZab1mq2}


...
{ #DX4IPjgX}


expires
{ #IjDOwBx7}


...
{ #T8ot59yX}


redisDb
{ #GKmTwLM7}


dictEntry
{ #hTmOQCQu}


redisObject
{ #SBwrZ1ho}


StringObject
"a"
{ #VbjAElec}


StringObject
"a"
{ #fl6xALeu}


StringObject
"a"
{ #oaz7JKZF}


StringObject
"a"
{ #rkS0DmJ1}


StringObject
name
{ #URyRDitA}


StringObject
"author"
{ #1dqboDyp}


StringObject
"publisher"
{ #ROMR4w5Y}


StringObject:
"Redis in Action"
{ #fCqHTyZM}


StringObject
"Josiah L. Carlson"
{ #vz6kud86}


StringObject
"Manning"
{ #tGRsZM1X}


＊key－－－＞
StirngObject
"bookHash:ISBN"
{ #n1fRv1AD}


＊key－－－＞
redisObject
"UserSesion:userId"
{ #v4gYN90n}


StringObject
"XXXXXX:XXXX:XXXX"
{ #BQLCek79}


db0
{ #A1WmXwUy}


redisServer
{ #eLJdFKUL}


db1
{ #gpP3N5cW}


sdshdr
{ #xpHmPLZB}


ｂｕｆ
{ #lh8PwB5A}


len
{ #os04Y6KK}


free
{ #GmSzGbKz}


buf[0] : 0 1 0 1 0 1 01
{ #SFToEI7D}


buf[1] : 0 1 0 1 0 1 01
{ #suQWrIiB}


buf[3] : 空字符
{ #VZmioyda}


＊key－－－＞
redisObject
"bitmap"
{ #EJSjwZ9o}


＊key---＞
StringObject
"intset"
{ #O82Vq2i9}


intset
{ #sN2KUnTS}


encoding
{ #Bkg1bZaV}


length
{ #SzNorbDG}


contents
{ #DlYpM5Ik}


字符串
{ #nhlGO0wx}


HashObject
{ #pqbJPVBd}


ListObject
{ #J1hfRoKO}


位图
{ #qyaGUmwC}


整型数组
{ #YbgHSiwh}


0  1  12 133 155
{ #TIUM5bFj}


注: 一个字节数组为8位
对于位图的相关操作会
进行对把取余得出index和offset
{ #yl7FGY3N}


＊value
{ #ZwVafMkC}


＊value
redisObject
{ #b3R9t9nY}


＊value
{ #x0SeVN1J}


dictht
{ #tS76xn1K}


type
{ #7CI3Y19v}


rehashidx: 
标志哈希操作是否完成
{ #CejrSY8M}


ht
{ #m1dR5Tmq}


dictEntry
{ #MoyiEhND}


dictEntry
{ #TZu60bN7}


dictEntry
{ #G0n1PoHX}


dictEntry
{ #CaYEvY5z}


null
{ #xThV6ond}


null
{ #CzSbXdix}


null
{ #sXSa88yK}


null
{ #LB1nOGwu}


null
{ #Dnf4axEQ}


dictEntry*[4]
{ #XTKeWFes}


0
{ #sUco6Vgt}


1
{ #Vu1P6TKY}


2
{ #sFECZAvt}


3
{ #n967Lpk2}


dictEntry*[4]
{ #CAMi9VuG}


0
{ #yXP248WL}


1
{ #QJ861Cvr}


2
{ #t7QVB5oK}


3
{ #qzDnezvq}


4
{ #aE097CAv}


这里长度很短，数量很少，就是压缩数组
{ #4lNsUtmv}


type: Reis_ZIPList
{ #Cmq3sYJI}


encoding: 
REDIS_ENCODING_ZIPLIST
{ #exQyBly9}


*ptr
{ #v1tNQO48}


＊value--->
RedisObject
{ #DzZYFEYo}


type: REDIS_bitmap
{ #3YbxG8Sr}


*PTR
{ #jHb7pNQE}


encoding: 
REDIS_ENCODING_bitmap
{ #jkuZ16OS}


＊key
{ #WUwvbRIv}


redisObject
{ #VhApUUS4}


type: Reis_List
{ #viY0jVX8}


encoding: 
REDIS_ENCODING_LINKEDLIST
{ #CSSV4ChV}


*ptr
{ #UHYz2A3F}


sdshdr
{ #mrfVZkKb}


free
{ #HWvUCRts}


len
{ #mZM6hOcf}


ptr
{ #cscHoNvp}


RedisObject
{ #5vAydtUz}


type: REDIS_STRING
{ #JQxeLrrQ}


*PTR
{ #JU0DGCLK}


encoding: 
REDIS_ENCODING_EMBSTR
{ #Mb8oZN7v}


char[] ：keyList
{ #lbx0a4bH}


ｚｌ
ｅｎｄ
{ #ZJDzKrVe}


ｚｌ
ｔａｉｌ
{ #AZyzCST0}


ｚｌ
ｂｙｔｅ
{ #WhgXsk81}


ｚｌ
ｌｅｎ
{ #C2tEa2dJ}


typedef struct listNode {
{ #1w3iomM0}


struct listNode *prev;
{ #EP6OMU6Z}


struct listNode *next;
{ #PIBnKjPC}


void *value;
{ #0blG5AtU}


} listNode;
{ #LD9RkOp9}


５
{ #O5okN0hP}


＊key---＞
StringObject
"hash"
{ #R8kkSyHo}


dictEntry
{ #gcNfiGnh}


null
{ #AE3JGZ3l}


redisObject
{ #8rG5S21Y}


type: Reis_set
{ #W2hFbrsV}


encoding: 
REDIS_ENCODING_ht
{ #rN3HT22N}


*ptr
{ #bsiz6Pb6}


dict
{ #8T9xzwxz}


entry－－－＞
{ #BMkcuJ9B}


StringObject
"intset"
{ #UUE1PeV0}


typedef struct dict {
{ #We65LcLp}


dictEntry **table;
{ #mtZcVkq0}


dictType *type;
{ #HNXNOyDR}


unsigned long size;
{ #xUHQTrxl}


unsigned long sizemask;
{ #mQZX3I4F}


unsigned long used;
{ #I0rkruUp}


void *privdata;
{ #wlXGwow6}


} dict;
{ #VifDN2Nt}


RedisObject
{ #mXLu1BSi}


type: REDIS_STRING
{ #pScBphiD}


*PTR
{ #HSoeU9SP}


encoding: 
REDIS_ENCODING_EMBSTR
{ #PKU16Pgd}


typedef struct dictEntry {
{ #uJIh6IA1}


void *key;
{ #1RL2YYxt}


void *val;
{ #8RlBi7TL}


struct dictEntry *next;
{ #7kX9uC1p}


} dictEntry;
{ #6vWvCCws}


＊key
{ #ZjC9Jrzs}


＊value
{ #AtI9Yd55}


＊next
{ #nStXmfVH}


dictEntry
{ #VABwbVDz}


RedisObject
{ #QigSeH1X}


type: REDIS_STRING
{ #ynY4KNq1}


*PTR
{ #fyjZtYC4}


encoding: 
REDIS_ENCODING_EMBSTR
{ #xpeaFvEz}


dictEntry
{ #GcWD3SFe}


＊value--->
RedisObject
{ #4OsmZ1fN}


＊value--->
RedisObject
{ #gCS0waOf}


５
{ #vXhMEXOy}


redisObject
{ #zYpB0PeV}


type: Reis_ZSET
{ #EmG93E2N}


encoding: 
REDIS_ENCODING_SKIPLIST
{ #FvKXYsMK}


*ptr
{ #mgyDpSXh}


zset
{ #WU9WUpoq}


dict
{ #7Sgpj5Xh}


zsl
{ #biB3GoZo}


ht
{ #Qyf6JLlh}


dict
{ #fxVg4gaf}


dictht
{ #zJPXOqph}


table
{ #izm1B0r1}


entry－－＞
StringObjetct
{ #bWwA987y}


5.0
{ #iVUSXIVz}


entry－－＞
StringObjetct
{ #jBDh3pjy}


6.0
{ #9uBJl3dV}


dictEntry［］
{ #G9EWaYa4}


假装这里长度>64
{ #91yNR2M1}


saveparams
{ #H8JG3Q2C}


saveparams[0]
{ #DNDKzZVy}


seconds 900
{ #zvxvEaLU}


changes 1
{ #WyfxCZmT}


saveparams[0]
{ #goQhrWuW}


seconds 300
{ #t4hIcOVe}


changes 10
{ #wU351eJs}


saveparams[0]
{ #Ujzci6uu}


seconds 60
{ #YzP7SiA1}


changes 10000
{ #cMffEm6Q}


#Redis/精图 : 配置加载原理
{ #bHbWZGUp}


dirty
{ #OzdBm8L1}


lastsave
{ #s9rJtv6A}


dictEntry*[4]
{ #KOnZVaXc}


0
{ #gSdmyhz5}


1
{ #JDBVnZN1}


2
{ #WQ3GLRDF}


3
{ #cX3NAO8W}


4
{ #yiMMI4Kt}


５
{ #SCQRiD4n}


５
{ #79McA9yi}


dictEntry*[4]
{ #KkHnAzpr}


0
{ #UgLGPw96}


1
{ #e2vxCKEs}


2
{ #zDOp1iJD}


3
{ #cXBom2Xh}


4
{ #5gtbJy7C}


５
{ #BRcyNHon}


５
{ #fMMRzGoj}



# Embedded files
7513d68bce49b20871c674b3e84774a8974c08c9: [[Pasted Image 20230708163006_101.png]]

