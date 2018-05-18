BOOST_DIR := /home/nik/tum/thesis/boost_1_66_0/boost
BOOST_LIB_DIR := $(BOOST_DIR)
BOOST_INC_DIR := $(BOOST_DIR)
TF_INC := $(shell python -c 'import tensorflow as tf; print(tf.sysconfig.get_include())')
TF_LIB=$(shell python -c 'import tensorflow as tf; print(tf.sysconfig.get_lib())')
TF_CFLAGS=($(shell python -c 'import tensorflow as tf; print(" ".join(tf.sysconfig.get_compile_flags()))') )
TF_LFLAGS=($(shell python -c 'import tensorflow as tf; print(" ".join(tf.sysconfig.get_link_flags()))') )

LDFLAGS := -Wl,--no-as-needed,-rpath,$(BOOST_LIB_DIR) -D_GLIBCXX_USE_CXX11_ABI=0

all: pose_to_heatmap.so zero_out_channels.so render_pose.so render_objects.so

pose_to_heatmap.so: pose_to_heatmap.cc
	g++ -std=c++11 $(LDFLAGS) -shared -I$(BOOST_INC_DIR) `pkg-config --cflags --libs opencv` pose_to_heatmap.cc -o pose_to_heatmap.so -fPIC -I $(TF_INC) -I $(TF_INC)/external/nsync/public -O2 -L$(BOOST_LIB_DIR) -lboost_system -lboost_filesystem -lboost_thread -L$(TF_LIB) -ltensorflow_framework

zero_out_channels.so: zero_out_channels.cc
	g++ -std=c++11 $(LDFLAGS) -shared zero_out_channels.cc -o zero_out_channels.so -fPIC -I $(TF_INC) -I $(TF_INC)/external/nsync/public -O2 -L$(TF_LIB) -ltensorflow_framework

render_pose.so: render_pose.cc pose_utils.hpp
	g++ -std=c++11 $(LDFLAGS) -shared -I$(BOOST_INC_DIR) `pkg-config --cflags --libs opencv` render_pose.cc -o render_pose.so -fPIC -I $(TF_INC) -I $(TF_INC)/external/nsync/public -O2 -L$(BOOST_LIB_DIR) -lboost_system -lboost_filesystem -lboost_thread -L$(TF_LIB) -ltensorflow_framework

render_objects.so: render_objects.cc
	g++ -std=c++11 $(LDFLAGS) -shared -I$(BOOST_INC_DIR) `pkg-config --cflags --libs opencv` render_objects.cc -o render_objects.so -fPIC -I $(TF_INC) -I $(TF_INC)/external/nsync/public -O2 -L$(BOOST_LIB_DIR) -lboost_system -lboost_filesystem -lboost_thread -L$(TF_LIB) -ltensorflow_framework
