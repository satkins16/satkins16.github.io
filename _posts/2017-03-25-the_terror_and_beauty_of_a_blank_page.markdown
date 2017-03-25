---
layout: post
title:  "The Terror and Beauty of a Blank Page"
date:   2017-03-25 18:47:35 +0000
---


In college I minored in Journalism, and as someone who was getting into writing on a consistant basis, there was nothing scarier than a blank page. Well, it seems writing and coding have more than a few things in common. Up until now, the Learn curriciulum has been a healthy mix of coding with full-on training wheels and coding with the occassional assist. Well this was my first experience with coding with where it was like skydiving without a parachute. But honestly, it helped me to fly.

Opening up a directory with zero code for the first time was terrifying. But like with writing, I discovered the worst thing you can do is think about the massive project ahead as a whole, but rather move one step at a time. Just think of the next one or two things you have to do, do them, and like Avi said in a lecture I watched, "The next steps will reveal themselves." By the time I was a few minutes into my code, I realized the beauty of an empty page: I can do whatever I want! I could make anything I dreamed up real in a CLI app by using everything I've worked so hard at for the past almost two months. And that's exactly what I did.

I faced a lot of serious stumbling blocks. There were a few times I felt genuinely stumped. But as I've written about before, one of the greate things about Ruby is it's similarity to how we as humans think and speak when it comes to syntax and logic. So if you have this understanding, you can simply say, "How would I solve this problem using normal everyday logic?" and start trying different things. And honestly, you'll get there. I did!  The key is to not get frustrated, which is easier said than done sometimes. For this project specifically, the Nokogiri gem and scraping websites played a large role. I was scraping data from Rolling Stone Magazine's website, and they use a ton of javascript which I have not been largely exposed to yet. Because they were dealing with such a large list (100 Greatest Guitarists), they chose to have the site load only five or so guitarists at a time, loading more as the user scrolls down. This stumped me. For a while. But by just pushing forward and constantly playing with the website and my code, I realized that the base URL for the site stayed the same, while the name of the guitarist downcased with dashes in between the first and the last name was simply added to the end. So by iterating through my guitarist list and susbstituting these downcased and dashed names into the url, I was able to receive all the info I needed for each specific guitarist. There were some exceptions on top of that but I took care of those as well. And boy did it feel good to figure this out:


```
self.all.each do |guitarist|
      new_url = guitarist.name.downcase.gsub(" ", "-").gsub("b.b.", "b-b").gsub("edward", "eddie").gsub("j.", "j")
      if new_url == "jimi-hendrix"
        @website = Nokogiri::HTML(open("http://www.rollingstone.com/music/lists/100-greatest-guitarists-20111123/#{new_url}-20120705"))
        guitarist.blurb = @website.css(".collection-item").text
      elsif new_url == "hubert-sumlin"
        @website = Nokogiri::HTML(open("http://www.rollingstone.com/music/lists/100-greatest-guitarists-20111123/#{new_url}-20111205"))
        guitarist.blurb = @website.css(".collection-item").text
      elsif new_url == "eddie-hazel"
        @website = Nokogiri::HTML(open("http://www.rollingstone.com/music/lists/100-greatest-guitarists-20111123/#{new_url}-20111202"))
        guitarist.blurb = @website.css(".collection-item").text
      elsif new_url == "dimebag-darrell"
        begin
        @website = Nokogiri::HTML(open("http://www.rollingstone.com/music/lists/100-greatest-guitarists-20111123/#{new_url}-20111215"))
        guitarist.blurb = @website.css(".collection-item").text
        rescue
        end
      else
        begin
          @website = Nokogiri::HTML(open("http://www.rollingstone.com/music/lists/100-greatest-guitarists-20111123/#{new_url}-20111122"))
          guitarist.blurb = @website.css(".collection-item").text
        rescue
        end
      end
    end
```
		

I was also fully exposed to the wonder of the pry gem. This thing is a lifesaver to say the least. To be able to mix and match where my pry was, inside and out of methods, is a thing of beauty. I, without question, could not have even come close to doing this without it. And it's beautiful that this indisposable piece of code was written by a user, and not even part of the original language. Ah, the power of collaboration.

After it was all over, I felt a swell of pride, as usual. My code worked just as I hoped it would. I learned tons of new things, simply by using what I've learned, speaking with others, and searching the internet. This experience continues to be as rewarding as any professional endeavor I've ever embarked on. And so far, this was as good as it gets.
