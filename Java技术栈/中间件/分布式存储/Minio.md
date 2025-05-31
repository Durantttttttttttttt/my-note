# Minio

MinIO 本身并不是传统意义上的“数据中间件技术”，而是一款高性能、开源的对象存储系统，基于 Apache License v2.0 协议开发，兼容亚马逊 S3 接口。它主要用于存储和管理大规模非结构化数据（如图片、视频、日志文件、备份数据等），而不是直接作为数据处理或数据流转的中间件。

不过，如果从广义的数据中间件概念来看，MinIO 可以被视为数据存储和管理生态系统中的一部分，属于“数据存储中间件”或“分布式存储层”的范畴。数据中间件技术通常包括数据采集、存储、处理、传输和访问等多个环节。



MinIO Java SDK 是一个客户端工具，用于与 MinIO 服务器进行交互（如上传文件、下载文件、创建存储桶等操作）。这些操作本质上是通过 HTTP/HTTPS 协议完成的，而 SDK 本身并没有内置完整的 HTTP 客户端实现，而是选择依赖一个成熟的第三方库——OkHttp。



毕设中使用：

```java
<dependency>
    <groupId>com.squareup.okhttp3</groupId>
    <artifactId>okhttp</artifactId>
    <version>4.12.0</version> <!-- Latest stable as of March 2025 -->
</dependency>
<dependency>
    <groupId>io.minio</groupId>
    <artifactId>minio</artifactId>
    <version>8.5.11</version>
</dependency>
```

配置：

```java
minio:
  endpoint: http://47.105.115.37:9000
  access-key: admin
  secret-key: password123
  bucket: artwork-images
```

服务类：初始化创建minio对象，uploadFile方法定义上传文件

```java
@Service
public class MinioService {
    @Value("${minio.endpoint}")
    private String endpoint;
    @Value("${minio.access-key}")
    private String accessKey;
    @Value("${minio.secret-key}")
    private String secretKey;
    @Value("${minio.bucket}")
    private String bucketName;

    private MinioClient minioClient;

    @PostConstruct
    public void init() {
        minioClient = MinioClient.builder()
                .endpoint(endpoint)
                .credentials(accessKey, secretKey)
                .build();
        try {
            if (!minioClient.bucketExists(BucketExistsArgs.builder().bucket(bucketName).build())) {
                minioClient.makeBucket(MakeBucketArgs.builder().bucket(bucketName).build());
            }
        } catch (Exception e) {
            throw new RuntimeException("MinIO初始化失败", e);
        }
    }

    /**
     * 上传文件到minio中，并返回访问的地址
     * @param file
     * @return
     * @throws Exception
     */
    public String uploadFile(MultipartFile file) throws Exception {
        String fileName = UUID.randomUUID() + "_" + file.getOriginalFilename();
        minioClient.putObject(PutObjectArgs.builder()
                .bucket(bucketName)
                .object(fileName)
                .stream(file.getInputStream(), file.getSize(), -1)
                .contentType(file.getContentType())
                .build());
        return endpoint + "/" + bucketName + "/" + fileName;
    }

    public String getFileUrl(String fileName) {
        return endpoint + "/" + bucketName + "/" + fileName;
    }
}
```
