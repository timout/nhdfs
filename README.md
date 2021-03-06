nhdfs
========================

**Node.js Native HDFS library wrapper**

#### Native hdfs library: 

 - [Pivotal libhdfs3](https://github.com/apache/incubator-hawq/tree/master/depends/libhdfs3)
 

### Requirement

To build nhdfs the following is required

    Node.js(8.6+) the library uses ABI-stable N-API for building the native Addon.
    cmake (2.8+)                    http://www.cmake.org/
    boost (tested on 1.53+)         http://www.boost.org/
    google protobuf                 http://code.google.com/p/protobuf/
    libxml2                         http://www.xmlsoft.org/
    kerberos                        http://web.mit.edu/kerberos/
    libuuid                         http://sourceforge.net/projects/libuuid/
    libgsasl                        http://www.gnu.org/software/gsasl/
    openssl                         https://www.openssl.org/

### Usage

**Note:** 
1) the module must be installed before use and N-API must be enabled on the 
command-line by adding --napi-modules (no need that option starting Node.js 8.6.0).
2) For Mac users, openssl must be installed with brew


``` js
const createFS = require('nhdfs').createFS;

const fs = createFS({service:"namenode", port:9000});
fs.list(".").then((list) => {
    list.forEach((element) => {
        console.log(element);
    });
})
.catch( (err) => {
    console.log(err);
})
```

#### Ways to connect
- By defining LIBHDFS3_CONF env variable: path to libhdfs3 config file or to hdfs-site.xml.  
  or by defining HADOOP_CONF_DIR env variable: Module will check if it has hdfs-site.xml inside.  
  or by defining HADOOP_CONF_DIR env variable defined: Module will check if it has hdfs-site.xml inside.  
    ``` js
    const createFS = require('nhdfs').createFS;
    const fs = createFS({service:"nameservice"});
    ```
- By providing path to config fileHADOOP_CONF_DIR env variable defined. Module will check if it has hdfs-site.xml inside.
    ``` js
    const createFS = require('nhdfs').createFS;
    const fs = createFS({service:"nameservice1", configurationPath:'/opt/hadoop/conf/hdfs-site.xml'});
    ```
- By providing NameNode host and port
    ``` js
    const createFS = require('nhdfs').createFS;
    const fs = createFS({service:"namenodehost", port:9000});
    ```

See [examples](https://github.com/timout/nhdfs/tree/master/examples) for more usage.