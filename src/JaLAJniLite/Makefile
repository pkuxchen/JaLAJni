DEST = .
CC = gcc
CFLAGS = $(INCLUDE) $(LIB) 

JAVA_HOME = ../..


JNI_LAPACK_SRC = $(JAVA_HOME)/src/JaLAJniLite/jni_lapack
JNI_BLAS_SRC = $(JAVA_HOME)/src/JaLAJniLite/jni_blas

INCLUDE = -I$(JNI_BLAS_SRC)/c/include \
	-I$(JAVA_HOME)/include \
	-I$(JNI_LAPACK_SRC)/c/include
LIB = -L/usr/local/lib 
C_SRC_LAPACK = $(JNI_LAPACK_SRC)/c/jniLAPACK.c
C_SRC_BLAS = $(JNI_BLAS_SRC)/c/jniCBLAS.c
DYLIB_LAPACK = $(JAVA_HOME)/lib/liblapack_lite.dylib
DYLIB_BLAS = $(JAVA_HOME)/lib/libblas_lite.dylib
	

# For package JaLAJniLite
JC = javac
JFLAGS = -d
JAVA_SRC = $(JNI_LAPACK_SRC)/java/jniLAPACK.java $(JNI_BLAS_SRC)/java/jniCBLAS.java
PACKAGE = $(JAVA_HOME)/class/JaLAJniLite


all: $(PACKAGE) $(DYLIB_LAPACK) $(DYLIB_BLAS)

$(PACKAGE): $(JAVA_SRC)
	@mkdir -p $(@D)
	$(JC) $(JFLAGS) $(JAVA_HOME)/class $(JAVA_SRC)



$(DYLIB_LAPACK): $(C_SRC_LAPACK)
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -shared -fPIC $(C_SRC_LAPACK) -llapack -o $(DYLIB_LAPACK)

$(DYLIB_BLAS): $(C_SRC_BLAS) 
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -shared -fPIC $(C_SRC_BLAS) -lblas -o $(DYLIB_BLAS)

clean: 
	rm -fr $(JAVA_HOME)/class/JaLAJniLite
	rm -f $(JAVA_HOME)/lib/libblas_lite.dylib
	rm -f $(JAVA_HOME)/lib/liblapack_lite.dylib
	rm -f $(JAVA_HOME)/test/JaLAJniLite_tests/*.class
	rm -f $(JAVA_HOME)/test/JaLAJniLite_tests/*.txt
