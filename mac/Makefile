TALK_INC_DIR = ./libjingle-0.6.14

AR = ar
CC = g++
CFLAGS = -Wall -fno-rtti -fno-exceptions -fvisibility=hidden -ffunction-sections -fdata-sections -gdwarf-2 -g3 -O0 -DHAMMER_TIME=1 -DLOGGING=1 -DFEATURE_ENABLE_SSL -DHASHNAMESPACE=__gnu_cxx -DPOSIX -DDISABLE_DYNAMIC_CAST -DHAVE_OPENSSL_SSL_H=1 -D_REENTRANT -DOSX -D_DEBUG -DEXPAT_RELATIVE_PATH -I$(TALK_INC_DIR) 
LDFLAGS = -lexpat -lssl -lcrypto -framework CoreFoundation -framework Carbon -framework Security -framework SystemConfiguration 

OBJS_DIR = ./obj
LIB_SRCS =
include libjingle_build.mk
LIB_OBJS = ${LIB_SRCS:%.cc=$(OBJS_DIR)/%.o}


APP_SRCS =
include app_build.mk
APP_OBJS = ${APP_SRCS:%.cpp=$(OBJS_DIR)/%.o}

LIB = libjingle.a
TARGET = ProbICE

$(OBJS_DIR)/%.o : %.c
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c -o $@ $<

$(OBJS_DIR)/%.o : %.cc
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c -o $@ $<

$(OBJS_DIR)/%.o : %.cpp
	@mkdir -p $(@D)
	$(CC) $(CFLAGS) -c -o $@ $<

$(LIB): $(LIB_OBJS)
	$(AR) -cr $@ $(LIB_OBJS)

$(TARGET): $(LIB) $(APP_OBJS)
	$(CC) -o $@ $(APP_OBJS) $(LIB) $(LDFLAGS)

.PHONY: clean all
all: $(TARGET)
clean:
	rm -f $(TARGET)
	rm -f $(LIB)
	rm -rf $(OBJS_DIR)
