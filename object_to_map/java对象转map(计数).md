# java对象转为map，可以用来统计某个对象中字段不为空的个数
---

`

 	/**
     * 获取对象字段有值的字段和
     * @param object
     * @return
     */
    private int objectFields(Object object){
        int num=0;
        Field[] fields=object.getClass().getDeclaredFields();
        if(fields!=null && fields.length>0){
            for(int i=0;i<fields.length;i++){
                try{
                    boolean accessFlag = fields[i].isAccessible();
                    fields[i].setAccessible(true);
                    Object o = fields[i].get(object);
                    if (o != null && !StringUtils.isEmpty(o.toString()))
                        num+=1;
                    fields[i].setAccessible(accessFlag);
                }catch (Exception e){
                    logger.info("获取人事档案完整度失败!", e);
                }
            }
        }
        return num;
    }

`