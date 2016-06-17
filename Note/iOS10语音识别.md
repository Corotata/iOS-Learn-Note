ios10提供了语音识别，Session 509

大致代码实现如下：

~~~

//请求权限
- (void)askPermission{

    [SFSpeechRecognizer requestAuthorization:^(SFSpeechRecognizerAuthorizationStatus status) {
        
        switch (status) {
            case SFSpeechRecognizerAuthorizationStatusAuthorized:{
                
                
                NSString *path = [[NSBundle mainBundle]pathForResource:@"老婆槽点.m4a" ofType:nil];
                NSURL *url = [NSURL fileURLWithPath:path];
                [self recognizeFileURL:url];
                
                
                NSLog(@"Good to go");
                break;
            }
            
            case SFSpeechRecognizerAuthorizationStatusDenied:{
                NSLog(@"user said no");
                break;
            }
            case SFSpeechRecognizerAuthorizationStatusRestricted:{
                  NSLog(@"Device isnot permitted");
                break;
            }
            case SFSpeechRecognizerAuthorizationStatusNotDetermined:{
                NSLog(@"Do not know yet");
                break;
            }
                
            default:
                break;
        }
    }];

}



//通过一个URL进行语音识别
- (void)recognizeFileURL:(NSURL *)url {
    SFSpeechRecognizer *recognizer = [[SFSpeechRecognizer alloc]init];
    if (!recognizer.isAvailable) {
        return;
    }

    
    SFSpeechURLRecognitionRequest *request = [[SFSpeechURLRecognitionRequest alloc]initWithURL:url];
    [recognizer recognitionTaskWithRequest:request resultHandler:^(SFSpeechRecognitionResult * _Nullable result, NSError * _Nullable error) {
        if(result == nil) return;
        
        if (result.isFinal) {
            NSArray *array = result.transcriptions;
            for (SFTranscription *scr in array) {
                 NSLog(@"File said :%@",scr.formattedString);
            }
//            NSLog(@"File said :%@",result.transcriptions);
        }
        
        
    }];

}


~~~