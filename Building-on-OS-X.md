BitShares OS X Build Instructions
===============================

1. Install XCode and its command line tools by following the instructions here: https://guide.macports.org/#installing.xcode. 
   In OS X 10.11 (El Capitan) and newer, you will be prompted to install developer tools when running a devloper command in the terminal. This step may not be needed.


2. Install Homebrew by following the instructions here: http://brew.sh/

3. Initialize Homebrew:
   ```
   brew doctor
   brew update
   ```

4. Install dependencies:
   ```
   brew install boost cmake git openssl autoconf automake libtool 
   brew link --force openssl 
   ```

5. *Optional.* To support importing Bitcoin wallet files:
   ```
   brew install berkeley-db
   ```

6. *Optional.* To use TCMalloc in LevelDB:
   ```
   brew install google-perftools
   ```

7. Clone the Bitshares repository:
   ```
   git clone https://github.com/bitshares/bitshares-core.git
   cd bitshares-core
   ```

8. Build BitShares:
   ```
   git submodule update --init --recursive
   cmake .
   make
   ```
Notes:
As mentioned elsewhere, Bitshares depends on the third-party libraries "Boost" and "OpenSSL". These libraries need to be in certain version ranges. At the moment, Boost needs to be between 1.57 and 1.65. OpenSSL needs to be in the 1.0.x range.

Boost:
You can check which version(s) of boost you have by asking brew:
   ```
   brew search boost
   ```
To install another version of Boost (such as 1.60):
   ```
   brew install boost@1.60
   ```

OpenSSL:
You may have an older version of OpenSSL than is required. If so, have brew get the latest:
   ```
   brew upgrade openssl
   ```

Compiling with these new versions:
We must now tell cmake where these libraries are. Instead of the "cmake ." mentioned above, we use:
   ```
   cmake -DBOOST_ROOT=/usr/local/opt/boost@1.60 -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl .
   ```
and then proceed with the normal
   ```
   make
   ```