#Indroduction

This repository is a clone of liamb315's repository called: "XeonPhiTutorials". It contains code from the book called: "Intel Xeon Phi Coprocessor High-Performance Programming". The origional repository (provided it isn't updated in the future) contains identical code to the examples from the book. This is great, and stops you from having to copy and paste them. However, this book was published in 2013, and as of the time of writing this, it's 2016. So most of the icc compiler flags have been depricated. The problems with this book that I found, is that:

1: All the compiler flags have been depricated. (not really the books fault, after all, it is a book and can't be updated.)

2: It doesn't supply any real makefiles.

3: And it doesn't give any insight into how to set up a development environment for the Xeon Phi, or what errors ICC will throw at you.

Honestly, if I can write some more detailed README files and it saves someone a few minutes by having a look at what I've done, then this repo will have been worth it.

#Build Intructions

###Step 1

Make sure some version of the Intel C compiler and all of its libraries are installed on the computer you'll be working on. This is often taken care of by the system administrator.

###Step 2

Ensure your enviroment is set up for compiling. This means that icc and all its respective libraries are on your path. A symptom of them not being on your path is typing icc, and icc not being found. Getting this all set up is a long process, and hence Intel has given a script which does it all for you. It can be found in the Intel folder somewhere like here:

/opt/intel/composer_xe_2013/bin/compilervars.sh

or here:

/opt/intel/compilers_and_libraries/linux/bin/compilervars.sh

Since all the paths which are added are erased after each session, it is suggested that you add something like: (if your path is the latter)

if [ -e /opt/intel/compilers_and_libraries/linux/bin/compilervars.sh ]; then
	. /opt/intel/compilers_and_libraries/linux/bin/compilervars.sh intel64
fi

to your .bashrc file. This will, on startup, check for the script from Intel, and if it exists, run it for an Intel 64 bit cpu.

###Step 3

Make your program. If you're just starting off, I recommend just entering the Ch2 directory of this repo, and typing:

make all

which will make all the example programs in chapter 2 of the "Intel Xeon Phi Coprocessor High-Performance Programming" textbook. Otherwise, just make any program for the phi.

###Step 4

Load your program onto the Phi with a command like: scp a.out uqjscola@mic0:/~ to use scp to move your file onto the phi.

###Step 5

Make sure your LD_LIBRARY_PATH environmental variable (in your linux system running on the phi) is pointing to crucial runtime libraries on the Xeon Phi. If you're using OpenMP, then chances are that you'll be notified that you're missing the file libiomp5.so if you try to run your code at this point. To fix this, use scp again to copy these libraries over. For example, libiomp5.so is found at: ...... on the computer I'm using.

###Step 6

Now that your environment is set up, if you try to run your file, it should work perfectly.
