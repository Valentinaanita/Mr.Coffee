# Mr.Coffee
The misadventures of Mr.Coffee


import SwiftUI
import PlaygroundSupport
import UIKit
import AVFoundation

var Image1 = UIImageView(image: UIImage(named:"Image1.jpeg"))

var Image2 = UIImageView(image: UIImage(named:"Image2.jpeg"))

var Text2 = UILabel(frame: CGRect(x: 250, y: 600, width: 300, height: 100))

var Image3 = UIImageView(image: UIImage(named:"Image3.jpeg"))

var Text3 = UILabel(frame: CGRect(x: 250, y: 600, width: 300, height: 100))

var IntroText = UILabel(frame: CGRect(x: 250, y: 600, width: 300, height: 100))
let SkipText = UILabel(frame: CGRect(x: 250, y: 700, width: 300, height: 100))
let EndChap = UILabel(frame: CGRect(x: 250, y: 700, width: 300, height: 100))

Image2.alpha = 0.0
Image3.alpha = 0.0

var touchesCounter = 0

SkipText.text = "TAP TO CONTINUE"
SkipText.alpha = 1.0
SkipText.font = UIFont.systemFont(ofSize: 16)
SkipText.textAlignment = .center
SkipText.textColor = .white
SkipText.numberOfLines = 5
SkipText.font = UIFont(name: "Futura", size: 15)

EndChap.text = "CHAPTER 1 END"
EndChap.alpha = 1.0
EndChap.font = UIFont.systemFont(ofSize: 16)
EndChap.textAlignment = .center
EndChap.textColor = .white
EndChap.numberOfLines = 5
EndChap.font = UIFont(name: "Futura", size: 15)

IntroText.text = "This is a story about an ordinary man, with an ordinary job.\n His name was Mr. Coffee."
IntroText.alpha = 0.0
IntroText.font = UIFont.systemFont(ofSize: 16)
IntroText.textAlignment = .center
IntroText.textColor = .white
IntroText.numberOfLines = 5
IntroText.font = UIFont(name: "Futura", size: 15)

Text2.text = "Mr. Coffee lived an ordinary life: gallons of coffee was running through his veins as FUEL and plenty of protein bars were CATALYSTS for his body."
Text2.alpha = 0.0
Text2.font = UIFont.systemFont(ofSize: 16)
Text2.textAlignment = .center
Text2.textColor = .white
Text2.numberOfLines = 5
Text2.font = UIFont(name: "Futura", size: 15)

Text3.text = "When he was a little cup he had many interests and dreams, but as the rigid Owl and wealthy Pig said:\n \"Don't waste your time, it passes by! You have to produce, consume and die!"
Text3.alpha = 0.0
Text3.font = UIFont.systemFont(ofSize: 16)
Text3.textAlignment = .center
Text3.textColor = .white
Text3.numberOfLines = 6
Text3.font = UIFont(name: "Futura", size: 15)



class MyView: UIView {
    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        super.touchesBegan(touches, with: event)
        
        if touchesCounter == 0 {
            //play audio
            SkipText.removeFromSuperview()
            player.play()
            //play voice1
            narratorPlayer1.play()
            UIView.transition(with: self, duration: 9, options: .transitionCrossDissolve, animations: {
                Image1.alpha = 1.0;
                IntroText.alpha = 1.0
            }, completion: {_ in
                UIView.transition(with: MainView, duration: 1, options: .transitionCrossDissolve, animations: {
                    Image1.alpha = 1.0
                })
                
                MainView.addSubview(SkipText)
            })
        } else if touchesCounter == 1 {
            
            SkipText.removeFromSuperview()
            
            UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve, animations: {
                IntroText.alpha = 0.0; Image1.alpha = 0.0
            }) { _ in
                Image1.removeFromSuperview()
                IntroText.removeFromSuperview()

                UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                    Image2.alpha = 1.0
                    Text2.alpha = 1.0

                }
                
                    completion: { _ in
                    narratorPlayer2.play()
                    UIView.transition(with: self, duration: 11, options: .transitionCrossDissolve, animations: {
                        
                        
                    })
                        MainView.addSubview(SkipText)
                }
                
                
                
            }
        } else if touchesCounter == 2 {
            
            SkipText.removeFromSuperview()
            
           UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve, animations: {
               Text2.alpha = 0.0; Image2.alpha = 0.0
           }) { _ in
               Image2.removeFromSuperview()
               Text2.removeFromSuperview()

               UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                   Image3.alpha = 1.0
                   Text3.alpha = 1.0
               } completion: { _ in
                   narratorPlayer3.play()
                   
                   UIView.transition(with: self, duration: 15, options: .transitionCrossDissolve, animations: {
                       
                   })
                   MainView.addSubview(EndChap)
               }
           }
       }
        
        touchesCounter += 1
    }
}

let MainView = MyView(frame: CGRect(x: 0, y: 0, width: 1090, height: 900))
MainView.backgroundColor = .black

PlaygroundPage.current.setLiveView(MainView)

MainView.addSubview(Image1)
MainView.addSubview(IntroText)

MainView.addSubview(Image2)
MainView.addSubview(Text2)

MainView.addSubview(Image3)
MainView.addSubview(Text3)

var url = Bundle.main.url(forResource: "The Coffee Waltz", withExtension: "wav")
//gets the filepath for the audio track in an URL format
var urlVoice1 = Bundle.main.url(forResource: "Narrator1", withExtension: "wav")
var urlVoice2 = Bundle.main.url(forResource: "Narrator2", withExtension: "wav")
var urlVoice3 = Bundle.main.url(forResource: "Narrator3", withExtension: "wav")

var player = try AVAudioPlayer(contentsOf: (url)!)
//creates an audio player and plays the track linked with the URL

var narratorPlayer1 = try AVAudioPlayer(contentsOf: (urlVoice1)!)
var narratorPlayer2 = try AVAudioPlayer(contentsOf: (urlVoice2)!)
var narratorPlayer3 = try AVAudioPlayer(contentsOf: (urlVoice3)!)

UIView.transition(with: MainView, duration: 1.5, options: .transitionCrossDissolve, animations: {
    Image1.alpha = 1.0
    MainView.addSubview(SkipText)
})


//: [Next](@next)
  
  
  
  -------------------------------------------------------------------------------------------------------------------
  
  
  
  
  
  //: [Previous](@previous)
import SwiftUI
import PlaygroundSupport
import UIKit
import AVFoundation

var Image4 = UIImageView(image: UIImage(named:"Image4.jpeg"))
var Text4 = UILabel(frame: CGRect(x: 150, y: 600, width: 500, height: 100))

var Image5 = UIImageView(image: UIImage(named:"Image5.jpeg"))
var Text5 = UILabel(frame: CGRect(x: 250, y: 600, width: 300, height: 100))

var Image6 = UIImageView(image: UIImage(named:"Image6.jpeg"))
var Text6 = UILabel(frame: CGRect(x: 150, y: 600, width: 500, height: 100))

var IntroText = UILabel(frame: CGRect(x: 250, y: 600, width: 300, height: 100))
let SkipText = UILabel( frame: CGRect(x: 250, y: 700, width: 300, height: 100))
let chapter2text = UILabel( frame: CGRect(x: 250, y: 350, width: 300, height: 100))
let EndChap = UILabel( frame: CGRect(x: 250, y: 700, width: 300, height: 100))

Image4.alpha = 0.0
Image5.alpha = 0.0
Image6.alpha = 0.0


var touchesCounter = 0

EndChap.text = "CHAPTER 2 END"
EndChap.alpha = 1.0
EndChap.font = UIFont.systemFont(ofSize: 16)
EndChap.textAlignment = .center
EndChap.textColor = .white
EndChap.numberOfLines = 5
EndChap.font = UIFont(name: "Futura", size: 15)


chapter2text.text = "CHAPTER 2"
chapter2text.alpha = 1.0
chapter2text.font = UIFont.systemFont(ofSize: 16)
chapter2text.textAlignment = .center
chapter2text.textColor = .white
chapter2text.numberOfLines = 5
chapter2text.font = UIFont(name: "Futura", size: 50)


SkipText.text = "TAP TO CONTINUE"
SkipText.alpha = 1.0
SkipText.font = UIFont.systemFont(ofSize: 16)
SkipText.textAlignment = .center
SkipText.textColor = .white
SkipText.numberOfLines = 5
SkipText.font = UIFont(name: "Futura", size: 15)


Text4.text = "So he left everything behind and started working for the ominous Vultus de Vulturis' company.\n But, as year passed, no matter how hard he tried, he would never be praised for it, nor would his income rise."
Text4.alpha = 0.0
Text4.font = UIFont.systemFont(ofSize: 16)
Text4.textAlignment = .center
Text4.textColor = .white
Text4.numberOfLines = 6
Text4.font = UIFont(name: "Futura", size: 15)

Text5.text = "\"Heh... You always work so hard, now take a break... and I will deal with your part!\" \n After the sly Rat's rattle, Mr. Coffee finally took his first break in years!"
Text5.alpha = 0.0
Text5.font = UIFont.systemFont(ofSize: 16)
Text5.textAlignment = .center
Text5.textColor = .white
Text5.numberOfLines = 6
Text5.font = UIFont(name: "Futura", size: 15)

Text6.text = "\"How could you even dare! Now pack your things and get out of here!\"\n As the ominous voice boomed through the halls Mr. Coffee realised he was tricked by the sly rat, who just wanted to earn the boss' favour!"
Text6.alpha = 0.0
Text6.font = UIFont.systemFont(ofSize: 16)
Text6.textAlignment = .center
Text6.textColor = .white
Text6.numberOfLines = 6
Text6.font = UIFont(name: "Futura", size: 15)



class MyView: UIView {
    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        super.touchesBegan(touches, with: event)
        
        if touchesCounter == 0 {

            player.play()
            chapter2text.removeFromSuperview()
            SkipText.removeFromSuperview()
            
            UIView.transition(with: self, duration: 0.5, options: .transitionCrossDissolve, animations: {
             
           }) { _ in
               
               UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                   Image4.alpha = 1.0
                   Text4.alpha = 1.0
               } completion: { _ in
                   
                   narratorPlayer4.play()

                   UIView.transition(with: self, duration: 14, options: .transitionCrossDissolve, animations: {
                       
                   })
                   
                   MainView.addSubview(SkipText)
               }
           }
       }  else if touchesCounter == 1 {
           
           SkipText.removeFromSuperview()
           
           UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve, animations: {
               Text4.alpha = 0.0; Image4.alpha = 0.0
           }) { _ in
               Image4.removeFromSuperview()
               Text4.removeFromSuperview()

               UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                   Image5.alpha = 1.0
                   Text5.alpha = 1.0
               } completion: { _ in
                   narratorPlayer5.play()
                   UIView.transition(with: self, duration: 13, options: .transitionCrossDissolve, animations: {
                       
                   })
                   
                   MainView.addSubview(SkipText)
               }
           }
       }    else if touchesCounter == 2 {
           
           SkipText.removeFromSuperview()
           
           UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve, animations: {
               Text5.alpha = 0.0; Image5.alpha = 0.0
           }) { _ in
               Image5.removeFromSuperview()
               Text5.removeFromSuperview()

               UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                   Image6.alpha = 1.0
                   Text6.alpha = 1.0
               } completion: { _ in
                   narratorPlayer6.play()
                   UIView.transition(with: self, duration: 13, options: .transitionCrossDissolve, animations: {
                       
                   })
                   
                   MainView.addSubview(EndChap)
                   
               }
           }
           
       }
        touchesCounter += 1
    }
}

let MainView = MyView(frame: CGRect(x: 0, y: 0, width: 1090, height: 900))
MainView.backgroundColor = .black

PlaygroundPage.current.setLiveView(MainView)


MainView.addSubview(Image4)
MainView.addSubview(Text4)

MainView.addSubview(Image5)
MainView.addSubview(Text5)

MainView.addSubview(Image6)
MainView.addSubview(Text6)

MainView.addSubview(chapter2text)
MainView.addSubview(SkipText)


var url = Bundle.main.url(forResource: "The Coffee Waltz", withExtension: "wav")
//gets the filepath for the audio track in an URL format
var player = try AVAudioPlayer(contentsOf: (url)!)
//creates an audio player and plays the track linked with the URL

var urlVoice4 = Bundle.main.url(forResource: "Narrator4", withExtension: "wav")
var urlVoice5 = Bundle.main.url(forResource: "Narrator5", withExtension: "wav")
var urlVoice6 = Bundle.main.url(forResource: "Narrator6", withExtension: "wav")

var narratorPlayer4 = try AVAudioPlayer(contentsOf: (urlVoice4)!)
var narratorPlayer5 = try AVAudioPlayer(contentsOf: (urlVoice5)!)
var narratorPlayer6 = try AVAudioPlayer(contentsOf: (urlVoice6)!)

UIView.transition(with: MainView, duration: 1.5, options: .transitionCrossDissolve, animations: {
   
})
//: [Next](@next)
  
  
  
  
  -------------------------------------------------------------------------------------------------------------------------
  
  
  
  
  
  //: [Previous](@previous)
import SwiftUI
import PlaygroundSupport
import UIKit
import AVFoundation

var Image7 = UIImageView(image: UIImage(named:"Image7.jpeg"))
var Text7 = UILabel(frame: CGRect(x: 150, y: 600, width: 500, height: 100))

var Image8 = UIImageView(image: UIImage(named:"Image8.jpeg"))
var Text8 = UILabel(frame: CGRect(x: 250, y: 600, width: 300, height: 100))

var Image9 = UIImageView(image: UIImage(named:"Image9.jpeg"))
var Text9 = UILabel(frame: CGRect(x: 150, y: 600, width: 500, height: 100))

var IntroText = UILabel(frame: CGRect(x: 250, y: 600, width: 300, height: 100))
let SkipText = UILabel( frame: CGRect(x: 250, y: 700, width: 300, height: 100))
let chapter2text = UILabel( frame: CGRect(x: 250, y: 350, width: 300, height: 100))
let EndChap = UILabel( frame: CGRect(x: 250, y: 700, width: 300, height: 100))

Image7.alpha = 0.0
Image8.alpha = 0.0
Image9.alpha = 0.0


var touchesCounter = 0

EndChap.text = "CHAPTER 2 END"
EndChap.alpha = 1.0
EndChap.font = UIFont.systemFont(ofSize: 16)
EndChap.textAlignment = .center
EndChap.textColor = .white
EndChap.numberOfLines = 5
EndChap.font = UIFont(name: "Futura", size: 15)

chapter2text.text = "CHAPTER 3"
chapter2text.alpha = 1.0
chapter2text.font = UIFont.systemFont(ofSize: 16)
chapter2text.textAlignment = .center
chapter2text.textColor = .white
chapter2text.numberOfLines = 5
chapter2text.font = UIFont(name: "Futura", size: 50)


SkipText.text = "TAP TO CONTINUE"
SkipText.alpha = 1.0
SkipText.font = UIFont.systemFont(ofSize: 16)
SkipText.textAlignment = .center
SkipText.textColor = .white
SkipText.numberOfLines = 5
SkipText.font = UIFont(name: "Futura", size: 15)


Text7.text = "With nothing left, the miserable Mr. Coffee drowned his sorrows in caffeine.\nAnd he drank, and drank, and drank...\nUntil his body collasped."
Text7.alpha = 0.0
Text7.font = UIFont.systemFont(ofSize: 16)
Text7.textAlignment = .center
Text7.textColor = .white
Text7.numberOfLines = 6
Text7.font = UIFont(name: "Futura", size: 15)

Text8.text = "As he passed out he had a mystical vision: a world made of beautiful, creative, challenging things...\nThings that he had been taught were useless."
Text8.alpha = 0.0
Text8.font = UIFont.systemFont(ofSize: 16)
Text8.textAlignment = .center
Text8.textColor = .white
Text8.numberOfLines = 6
Text8.font = UIFont(name: "Futura", size: 15)

Text9.text = "Now the renewed Mr. Coffee still drinks coffee... But in moderation!\nAnd you? Are you ready to take the first step on your life-changing journey?"
Text9.alpha = 0.0
Text9.font = UIFont.systemFont(ofSize: 16)
Text9.textAlignment = .center
Text9.textColor = .white
Text9.numberOfLines = 6
Text9.font = UIFont(name: "Futura", size: 15)



class MyView: UIView {
    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        super.touchesBegan(touches, with: event)
        
        if touchesCounter == 0 {
            //play audio
            player.play()
            chapter2text.removeFromSuperview()
            SkipText.removeFromSuperview()
            UIView.transition(with: self, duration: 0.5, options: .transitionCrossDissolve, animations: {
             
           }) { _ in
               

               UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                   Image7.alpha = 1.0
                   Text7.alpha = 1.0
               } completion: { _ in
                   
                   narratorPlayer7.play()
                   
                   UIView.transition(with: self, duration: 10, options: .transitionCrossDissolve, animations: {
                       
                   })
                   MainView.addSubview(SkipText)
               }
           }
       }  else if touchesCounter == 1 {
           
           SkipText.removeFromSuperview()
           
           UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve, animations: {
               Text7.alpha = 0.0; Image7.alpha = 0.0
           }) { _ in
               Image7.removeFromSuperview()
               Text7.removeFromSuperview()

               UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                   Image8.alpha = 1.0
                   Text8.alpha = 1.0
               } completion: { _ in
                   
                   narratorPlayer8.play()
                   
                   UIView.transition(with: self, duration: 10, options: .transitionCrossDissolve, animations: {
                       
                   })
            
                   MainView.addSubview(SkipText)
               }
           }
       }    else if touchesCounter == 2 {
           
           SkipText.removeFromSuperview()
           
           UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve, animations: {
               Text8.alpha = 0.0; Image8.alpha = 0.0
           }) { _ in
               Image8.removeFromSuperview()
               Text8.removeFromSuperview()

               UIView.transition(with: self, duration: 2, options: .transitionCrossDissolve) {
                   Image9.alpha = 1.0
                   Text9.alpha = 1.0
               } completion: { _ in
                   
                   narratorPlayer9.play()
                   
                   UIView.transition(with: self, duration: 11, options: .transitionCrossDissolve, animations: {
                       
                   })
               }
           }
           
       }
        touchesCounter += 1
    }
}

let MainView = MyView(frame: CGRect(x: 0, y: 0, width: 1090, height: 900))
MainView.backgroundColor = .black

PlaygroundPage.current.setLiveView(MainView)



MainView.addSubview(Image7)
MainView.addSubview(Text7)

MainView.addSubview(Image8)
MainView.addSubview(Text8)

MainView.addSubview(Image9)
MainView.addSubview(Text9)

MainView.addSubview(chapter2text)
MainView.addSubview(SkipText)


var url = Bundle.main.url(forResource: "The Coffee Waltz", withExtension: "wav")
//gets the filepath for the audio track in an URL format
var player = try AVAudioPlayer(contentsOf: (url)!)
//creates an audio player and plays the track linked with the URL

var urlVoice7 = Bundle.main.url(forResource: "Narrator7", withExtension: "wav")
var urlVoice8 = Bundle.main.url(forResource: "Narrator8", withExtension: "wav")
var urlVoice9 = Bundle.main.url(forResource: "Narrator9", withExtension: "wav")

var narratorPlayer7 = try AVAudioPlayer(contentsOf: (urlVoice7)!)
var narratorPlayer8 = try AVAudioPlayer(contentsOf: (urlVoice8)!)
var narratorPlayer9 = try AVAudioPlayer(contentsOf: (urlVoice9)!)

UIView.transition(with: MainView, duration: 1.5, options: .transitionCrossDissolve, animations: {
   
})


