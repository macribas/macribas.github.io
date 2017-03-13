How to identify the protocol in a Cloud Foundry Java application
================================================================

Sometimes you need to invoke other files in your Java Cloud Foundry application
(make AJAX calls or load JavaScript). If your app is working through HTTPS, and
you try to have the browser load another file through HTTP, it will break. So a
good practice is to try to identify which protocol is being used and form the
links accordingly.

You usually have access to the Request object and that has a method called
`getProtocol()`. In traditional web application server deployments, that is all
you need. Parse that string and you’re done. But in Cloud Foundry, because there
is a load balancer in front of your instances, that method always returns
`"HTTP/1.1"`.

To overcome that problem, Cloud Foundry inserts a header called
**"x-forwarded-proto”**. All you need to do is use the
`request.getHeader(“x-forwarded-proto”)` method and use the returned value. It
will either be `http` or `https`.
