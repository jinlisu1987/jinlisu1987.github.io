# spring redis 支持多个客户端

        JedisPoolConfig config = new JedisPoolConfig();
        config.setMaxIdle(20);
        config.setMinIdle(10);
        config.setMaxTotal(100);
        config.setMaxWaitMillis(5000);
        config.setTestOnBorrow(true);
        config.setTestOnReturn(true);
        JedisConnectionFactory factory = new JedisConnectionFactory();
        factory.setPoolConfig(config);
        factory.setTimeout(2000);
        factory.setHostName(oldRdisHostName);
        factory.setPort(Integer.valueOf(oldRdisPort));
        factory.afterPropertiesSet();// 最关键！！！！！！！
        oldRedisTemplate = new StringRedisTemplate(factory);
        oldRedisTemplate.hasKey("limit_item_id");
        
        ## 参考
        https://blog.csdn.net/wangh92/article/details/80311777
        
