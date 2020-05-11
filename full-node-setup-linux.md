# This is a tutorial on how to run a Full RasbyCoin Node
#
# Copy and paste each line one by one:

        sudo apt-get update
        sudo apt-get upgrade
        
        sudo apt-get install nano
        sudo apt-get install git
        sudo apt-get install cron
        
        sudo apt-get install git
 
        sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
 
        sudo apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-         dev libboost-thread-dev
 
        sudo apt-get install libboost-all-dev
 
        sudo apt-get install software-properties-common
 
        sudo add-apt-repository ppa:bitcoin/bitcoin
 
        sudo apt-get update
 
        sudo apt-get install libdb4.8-dev libdb4.8++-dev
 
        sudo apt-get install libminiupnpc-dev
 
        sudo apt-get install libzmq3-dev
 
        sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
 
        sudo apt-get install libqt4-dev libprotobuf-dev protobuf-compiler
        
        
        git clone https://github.com/rasbycoin-project/rasbycoin.git
        
        
        RASBYCOIN_ROOT=$(pwd)/rasbycoin
        
        BDB_PREFIX="${RASBYCOIN_ROOT}/db4"
        
        mkdir -p $BDB_PREFIX
        
        wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'
        
# Verify the integrity of the database software and install:
        
        echo '12edc0df75bf9abd7f82f821795bcee50f42cb2e5f76a6a281b85732798364ef db-4.8.30.NC.tar.gz' | sha256sum -c
        
        tar -xzvf db-4.8.30.NC.tar.gz
        
        cd db-4.8.30.NC/build_unix/
        
        ../dist/configure --enable-cxx --disable-shared --with-pic --prefix=$BDB_PREFIX
        
        make install
        
        
# Compile Rasbycoin     See: how-to-install-on-linux.md to fix possible issues

        cd $RASBYCOIN_ROOT
        
        cd src/leveldb
        sudo chmod +x build_detect_platform
        cd ..
        
        make -f makefile.unix
        
        sudo strip rasbycoind
        
        cd $home
        
        sudo adduser rasbycoin
        sudo usermod -g users rasbycoin
        sudo delgroup rasbycoin
        sudo chmod 0701 /home/rasbycoin
        sudo mkdir /home/rasbycoin/bin 

        sudo cp ~/rasbycoin/src/rasbycoind /home/rasbycoin/bin/rasbycoind
        sudo chown -R rasbycoin:users /home/rasbycoin/bin
        
        su rasbycoin
        
        cd $HOME
        mkdir .rasbycoin
        cd .rasbycoin
        
# See rasbycoin.conf in rasbycoin/ for instractions

        nano rasbycoin.conf
        
# save and exit by pressing <CTRL+x>

        chmod 0600 rasbycoin.conf
        
        cd ../bin
        ./rasbycoind -daemon
        
        crontab -e
# Add the following line below # comments

        @hourly /home/rasbycoin/bin/rasbycoind -daemon
        
# save and exit by pressing <CTRL+x>
        
