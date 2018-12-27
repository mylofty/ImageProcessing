INCLUDES = -I/home/dzm/opencv3_4/include
LIBS = -lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_imgcodecs
LIBDIRS = -L/home/dzm/opencv3_4/lib64
SOPATH = /home/dzm/opencv3_4/lib64
#mat.o : mat.cpp
#	g++ -o mat.o mat.cpp $(INCLUDES) $(LIBDIRS) $(LIBS)
all: pixel_scan.o mat.o
pixel_scan.o : pixel_scan.cpp
	g++ -o pixel_scan.o pixel_scan.cpp $(INCLUDES) $(LIBDIRS) $(LIBS) -Wl,-rpath=$(SOPATH)
mat.o : mat.cpp
	g++ -o mat.o mat.cpp $(INCLUDES) $(LIBDIRS) $(LIBS)

.PHONY: clean
clean:
	rm *.o
