# RasbyCoin
 RasbyCoin Project          https://rasbycoin.com
 
 
This is Build and Error Guide for RasbyCoin Compilation


# Install the dependencies :

    sudo apt-get update
    
    sudo apt-get install git
 
    sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
 
    sudo apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev     libboost-thread-dev
 
    sudo apt-get install libboost-all-dev
 
    sudo apt-get install software-properties-common
 
    sudo add-apt-repository ppa:bitcoin/bitcoin
 
    sudo apt-get update
 
    sudo apt-get install libdb4.8-dev libdb4.8++-dev
 
    sudo apt-get install libminiupnpc-dev
 
    sudo apt-get install libzmq3-dev
 
    sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
 
    sudo apt-get install libqt4-dev libprotobuf-dev protobuf-compiler
   
# Compile Daemon and Qt
   
    cd rasbycoin/src/leveldb
    sudo chmod +x build_detect_platform
    make clean
    make libleveldb.a libmemenv.a
   
To generate the daemon from code, run :
   
    cd /rasbycoin/src
    make -f makefile.unix
    
To compile rasbycoin-qt

    cd /rasbycoin
    qmake
    make
   
# Setup rasbycoin.conf in /home/.rasbycoin

    addnode=18.144.82.8 
    #
    #
    #
    #
    
    
    

# Possible Errors can be resolved with following solutions.

    Error: 
    Building LevelDB ...
    make[1]: Entering directory '/home/ubuntu/rasbycoin/src/leveldb'
    /bin/sh: 1: ./build_detect_platform: Permission denied
    Makefile:18: build_config.mk: No such file or directory
    make[1]: *** No rule to make target 'build_config.mk'. Stop.
    make[1]: Leaving directory '/home/ubuntu/rasbycoin/src/leveldb'
    makefile.unix:167: recipe for target 'leveldb/libleveldb.a' failed
    make: *** [leveldb/libleveldb.a] Error 2
     
# Solution:
    cd src/
    cd leveldb/
    sudo chmod +x build_detect_platform
    
### --------------------------------------------------------------------------------

    Error: 
    Building LevelDB ...
    make[1]: Entering directory '/home/ubuntu/rasbycoin/src/leveldb'
    /bin/sh: 1: ./build_detect_platform: Permission denied
    Makefile:18: build_config.mk: No such file or directory
    make[1]: *** No rule to make target 'build_config.mk'. Stop.
    make[1]: Leaving directory '/home/ubuntu/rasbycoin/src/leveldb'
    makefile.unix:164: recipe for target 'leveldb/libleveldb.a' failed
    make: *** [leveldb/libleveldb.a] Error 2

# Solution:

     cd /rasbycoin/src/leveldb
    make libleveldb.a libmemenv.a
    
### --------------------------------------------------------------------------------
 
    Error:
    > rasbcoiny/src/leveldb : make libleveldb.a libmemenv.a
    /bin/sh: 1: ./build_detect_platform: Permission denied
    Makefile:18: build_config.mk: No such file or directory
    make: *** No rule to make target 'build_config.mk'. Stop.
    
# Solution:

    > rasbycoin/src/leveldb : chmod +x build_detect_platform
    
    
### --------------------------------------------------------------------------------
    Error:
    version.cpp:33:23: fatal error: build.h: No such file or directory
    
# Solution:

    Move build.h from the rasbycoin/build to rasbycoin/src
    
    
### --------------------------------------------------------------------------------
    Error:
    fatal error: leveldb/db.h: No such file or directory
    
# Solution:

    sudo apt-get install libleveldb-dev
    
### --------------------------------------------------------------------------------
    Error:
    invalid application of ‘sizeof’ to incomplete type ‘boost::STATIC_ASSERTION_FAILURE<false>’ BOOST_STATIC_ASSERT_MSG(
    
# Solution:

Open the file ‘rpcrawtransaction.cpp’

    cd rasbycoin/src
    nano rpcrawtransaction.cpp
    
Search for this line (probably before ‘function createrawtransaction()’)

    const CScriptID& hash = boost::get<const CScriptID&>(address);
    
Change it to:

    const CScriptID& hash = boost::get<CScriptID>(address);
    
### --------------------------------------------------------------------------------

    Error:
    fatal error: miniupnpc/miniwget.h: No such file or directory
    
# Solution:

    sudo apt-get install libqt4-dev libminiupnpc-dev
    
### --------------------------------------------------------------------------------

    Error:
    leveldb.cpp:11:27: fatal error: memenv/memenv.h: No such file or directory
    compilation terminated.
    makefile.unix:176: recipe for target 'obj/leveldb.o' failed
    make: *** [obj/leveldb.o] Error 1
    
# Solution:

    cp -r leveldb/helpers/memenv/ /usr/include/memenv

   
###   --------------------------------------------------------------------------------
