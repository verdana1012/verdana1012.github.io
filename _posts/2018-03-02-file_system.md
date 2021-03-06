---
title: "File System"
categories: posts
tags:
  - etc
date: 2018-03-02 00:00:00 -0400
---


## [파일시스템]

파일 시스템(file system, 문화어: 파일체계)은 컴퓨터에서 파일이나 자료를  
쉽게 발견 및 접근할 수 있도록 보관 또는 조직하는 체제를 가리키는 말이다  


## [extended file system (확장 파일 시스템)]

### ext

리눅스 운영 체제를 목표로 만들어진 첫 번째 파일 시스템  
파일 최대크기 2GB, 호환성이 없다. =  분리 접근, 아이노드(inode) 수정,   
자료 수정 타임스탬프2 등의 기능을 지원하지 않으며,  
연결 리스트를 사용했기 때문에 사용하면 할수록 리스트가 뒤죽박죽이 되고 파일 시스템이 조각화된다는 단점이 있다.  
연결 리스트, 링크드 리스트(linked list)는 각 노드가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료 구조이다.  
ext2의 원형이다.


### ext2

ext의 문제를 해결하기 위해 나온 파일 시스템  
ext3가 개발되기 이전까지 가장 많이 사용된 파일 시스템으로 리눅스 파일 시스템, 대부분의 기능을 제공하는 파일 시스템이다.   
특히 ext2는 뛰어난 안정성과 속도로 가장 유명한 파일 시스템으로 자리 잡았고   
ext3 또한 ext2에 기반을 두어 개발되었다. 또한 쉽게 호환되며 업그레이드도 쉽게 설계되어 있다.  



### ext3

ext2 파일시스템에 저널링(Journaling)3을 지원하도록 확장된 파일시스템이다.   
ext3 파일 시스템은 또한 저널링을 할 때 체크섬을 검사하지 않는다.  
현재 리눅스에 가장 많이 사용되고 있다.  


### ext4

큰 파일 시스템(16TB) 까지의 파일을 지원.  
ext3 파일시스템을 확장한 파일시스템  
ext3 파일 시스템에 없었던 저널 체크섬 기능이 추가됨으로써, 파일 시스템 손상 가능성이 더 줄어들었다.  
ext 2,3에서 쓰이던 블록매핑(block mapping) 방식을 대체로 Extent라는 기능을 제공하고 다중블록할당  



### 블록매핑

가상 기억 장치를 구현하기 위해서 사상 정보의 양을 줄이는 방법으로 정보를 블록 단위로 묶어   
여러 개의 가상 기억 장치의 각 블록이 실기억 장치의 어느 곳에 위치하는지를 시스템이 관리하는 것.  


### Extent

어느 정도의 연속된 공간만 초기에 할당하고 그 양이 충분하지 않을 때 연속된 공간(extent)라 부르는 단위를 추가로 할당 대용량 파일 접근 속도 향상 및 단편화를 줄인다  


### 다중블록할당

이전파일시스템 : 새로운 데이터를 디스크로 쓸 필요가 생길 때, 블록 할당자(Block Allocator)는 데이터가 쓰여질 가용 공간을 결정  
Ext2,3 블록 할당자는 오직 한번에 한 개의 블록(4KB)만 할당 할 수 있음  
만약 시스템이 100MB의 가용공간이 필요하다면 Ext2/3 블록 할당자는 25600번 (100MB = 25600 블록)의 블록 할당 호출을 하게 됨   
Ext4의 다중 블록 할당 : Ext4는 매 호출마다 싱글 블럭을 할당하는 대신에   
한번의 호출로 많은 블록을 할당할 수 있는 다중 블록 할당자(multi block allocator)를 사용		  							



## [아이노드]

아이노드(inode)는 파일의 이름을 제외한 해당 파일의 모든 정보를 가지고 있다.   
파일 이름은 inode 번호와 함께 디렉토리 안에 저장된다.   
inode는 파일시스템의 가장 기본되는 단위이다.   
또한 각각을 구분할 수 있는 고유 번호를 가지고 파일의 테이터가 어느 블록에 어느 위치에 저장되어 있는지,   
파일에 대한 접근 권한, 파일의 최종 수정시간 그리고 파일의 종류등의 정보를 inode 테이블에 저장한다.   
inode 또한 실제로 존재하지는 않지만 시스템의 장치에 접근할 수 있는 특별한 장치 파일의 표현에도 사용된다.   
리눅스 시스템의 /dev 디렉토리 안에 위치하는 파일들이 그것들이다.   



## [journaled file system  (JFS - 저널링파일시스템)]

시스템 충돌이나 시스템 중단 시 하드 디스크 무결성을 유지시키기 위해 사용되는 파일 시스템.   
디스크의 데이터 영역에서 일어나는 모든 내용을 로그로 유지하면서 충돌이 발생하면 로그에 있는 메타 데이터로 유실 데이터를 다시 만들어 충돌 전으로 데이터를 되돌려 줄 뿐 아니라 저장되지 않은 데이터도 제자리에 저장한다.  

FS는 1990년에 처음 출시되었지만, 현재 리눅스에서 지원되는 버전은 나중에 개발된 JFS2다.  
1994년 실리콘 그래픽스 사는 고성능 XFS를 IRIX 운영체제에 도입했다.  
XFS는 2001년 리눅스로 이식되었다.   
아미가를 위해 1998년에 SFS(Smart File System)가 개발되었고,   
나중에 LGPL(GNU Lesser General Public License) 하에 공개되어 2005년부터 리눅스를 지원하기 시작했다.  


