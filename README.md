OAuthCore Static Library
========================

OAuth code from https://github.com/atebits/OAuthCore

Static library project setup from https://github.com/kstenerud/iOS-Universal-Framework

Usage
=====

Open up the XCode project. Build. Copy framework into your own project.

    #import <OAuthCore/OAuthCore.h>

    ...

    NSURL *url = [NSURL URLWithString:@"https://example.com/oauthendpoint"];
    NSString *method = @"POST";
    NSData *body = [NSData data];
    NSString *consumerKey = @"yourkey";
    NSString *consumerSecret = @"yoursecret";
    NSString *token = @"";
    NSString *tokenSecret = @"";

    NSString *oauthHeader = OAuthorizationHeader(url, method, body, consumerKey, consumerSecret, token, tokenSecret);
    NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
    [request addValue:oauthHeader forHTTPHeaderField:@"Authorization"];
    [request setHTTPMethod:method];
    [request setHTTPBody:body];
    [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue] completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {
        NSLog(@"Data: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);
    }];