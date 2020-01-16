See https://github.com/swagger-api/swagger-parser/tree/v2.0.11 for README info.

This is a fork that looks into a common wrapper on all requests and responses

All this fork does is put:

// Look into "data" wrapper
if (model instanceof ObjectSchema) {
    ObjectSchema op = (ObjectSchema) model;
    if (op.getProperties() != null && op.getProperties().containsKey("data")) {
        Schema underWrapper = op.getProperties().get("data");
        if (underWrapper != null) {
            mediaType.setSchema(underWrapper);
            model = underWrapper;
        }
    }
}
To both the request and response parsing inside:

swagger-parser-v3/src/main/java/io/swagger/v3/parser/util/InlineModelResolver.java
