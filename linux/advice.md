```
//    /**  
//     * 处理时间LocalDateTime转化异常  
//     */  
//    @ExceptionHandler(HttpMessageNotReadableException.class)  
//    public ResponseEntity<ApiResponse<Void>> handleHttpMessageNotReadable(HttpMessageNotReadableException ex) {  
//        String msg = "请求体解析失败";  
//        DateTimeParseException dtpe = findCause(ex, DateTimeParseException.class);  
//        if (dtpe != null) {  
//            msg = "时间格式错误，请使用 yyyy-MM-dd HH:mm:ss";//            return buildErrorResponse(HttpStatus.BAD_REQUEST, 400, msg, ex);  
//        }  
//  
//        InvalidFormatException ife = findCause(ex, InvalidFormatException.class);  
//        if (ife != null && ife.getTargetType() != null  
//            && LocalDateTime.class.isAssignableFrom(ife.getTargetType())) {  
//            msg = "时间格式错误，请使用 yyyy-MM-dd HH:mm:ss";//            return buildErrorResponse(HttpStatus.BAD_REQUEST, 400, msg, ex);  
//        }  
//        return buildErrorResponse(HttpStatus.BAD_REQUEST, 400, msg, ex);  
//    }
```

```
/**  
 * 寻找指定类型的异常 cause  
 */private static <T extends Throwable> T findCause(Throwable ex, Class<T> type) {  
    Throwable cur = ex;  
    while (cur != null) {  
        if (type.isInstance(cur)) {  
            return type.cast(cur);  
        }  
        cur = cur.getCause();  
    }  
    return null;  
}
```