# API Gateway CORS configuration module for Terraform

This is a slim Terraform module which creates an OPTIONS method and applies a CORS configuration for a resource in API Gateway.

Example: 
```
module "MyResourceCors" {
  source = "github.com/carrot/terraform-api-gateway-cors-module"
  resource_name = "MyResource"
  resource_id = "${aws_api_gateway_resource.MyResource.id}"
  rest_api_id = "${aws_api_gateway_rest_api.MyAPI.id}"
}
```

### Note:
Be sure to also set the `response_parameters` values on each of your Method Responses and Integration Responses.
Example:
```
resource "aws_api_gateway_method_response" "DemoPostMethodResponse200" {
  rest_api_id = "${aws_api_gateway_rest_api.API.id}"
  resource_id = "${aws_api_gateway_resource.Demo.id}"
  http_method = "${aws_api_gateway_method.DemoPost.http_method}"
  status_code = "200"
  response_models = {
    "application/json" = "Empty"
  }
  response_parameters = { "method.response.header.Access-Control-Allow-Origin" = "true" }
}
```
