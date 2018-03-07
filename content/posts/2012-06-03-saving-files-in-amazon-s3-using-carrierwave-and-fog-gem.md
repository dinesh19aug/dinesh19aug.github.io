---
title: Saving files in Amazon S3 using Carrierwave and Fog Gem
author: Dinesh
type: post
date: 2012-06-03T04:57:16+00:00
url: /2012/06/03/saving-files-in-amazon-s3-using-carrierwave-and-fog-gem/
reddit:
  - 'a:2:{s:5:"count";i:0;s:4:"time";i:1364811720;}'
  - 'a:2:{s:5:"count";i:0;s:4:"time";i:1364811720;}'
twitter_cards_summary_img_size:
  - 'a:6:{i:0;i:1265;i:1;i:431;i:2;i:3;i:3;s:25:"width="1265" height="431"";s:4:"bits";i:8;s:4:"mime";s:9:"image/png";}'
  - 'a:6:{i:0;i:1265;i:1;i:431;i:2;i:3;i:3;s:25:"width="1265" height="431"";s:4:"bits";i:8;s:4:"mime";s:9:"image/png";}'
dsq_thread_id:
  - 5292097444
  - 5292097444
categories:
  - Tech Notes

---
Long long time ago in a far far away land&#8230;.. I am just kidding. So I needed a gem to do file uploads(in my case images but you can upload anything) and I was looking at various options. <a title="Paperclip" href="https://github.com/thoughtbot/paperclip" target="_blank">Paperclip</a> is a popular option but there is a new kid on the block (so i read in various forums)&#8230; <a title="Carrierwave" href="https://github.com/jnicklas/carrierwave" target="_blank">Carrierwave</a>.

Now I have not used Paperclip but what I read was that <a title="Carrierwave" href="https://github.com/jnicklas/carrierwave" target="_blank">Carrierwave</a> is more flexible and powerful than <a title="Paperclip" href="https://github.com/thoughtbot/paperclip" target="_blank">Paperclip</a> so if are interested then keep reading. Now let me tell you that you may need to do some additional settings, I will not get into details because the wiki page of <a title="Carrierwave" href="https://github.com/jnicklas/carrierwave" target="_blank">Carrierwave</a> is pretty intensive. The purpose of writing this post is to highlight a couple of issue that I ran into and some settings which were not explained.

Step 1: Install the <a title="Carrierwave" href="https://github.com/jnicklas/carrierwave" target="_blank">Carrierwave</a> gem

**  gem install carrierwave**

Step 2: Update the gem file

gem carrierwave

Step 3: Now you need a uploader. This is the file which has all the settings like which folder the image will be saved, setting the image quality, caching etc. I wanted to call my uploader class as **ImageUploader**

**rails generate uploader ImageUploader**

Step 4: Install fog gem

**gem install fog**

Step 5: Update gem file

**gem &#8216;fog&#8217;, &#8216;~> 1.3.1&#8217;**

**bundle install**

Step 6: Choose the storage type

<span style="color:#0000ff;">class ImageUploader < CarrierWave::Uploader::Base</span>

<span style="color:#0000ff;">    <span style="color:#003366;"> storage :fog</span></span>

<span style="color:#0000ff;">end</span>

Step 7: Create model. Mine was called Photo so I create photo.rb. Notice the line number 10.

<span style="color:#000080;">class Photo < ActiveRecord::Base</span>

<span style="color:#800080;">#Attributes or fileds</span>
  
 <span style="color:#800080;">attr_accessible :image,:pic_name,:description,:albums_id</span>

<span style="color:#808080;">#associations</span>
  
 <span style="color:#800080;">belongs_to :albums</span>

<span style="color:#800080;"><span style="color:#808080;">#carrier wave</span> </span>
  
 <span style="color:#800080;">mount_uploader :image,</span>**ImageUploader**

<span style="color:#808080;">#Validations</span>
  
<span style="color:#800080;">validates :description,:pic_name,:albums_id, :presence=>true</span>
  
<span style="color:#800080;">validates_uniqueness_of :pic_name</span>
  
<span style="color:#000080;">end</span>

Step 7: How to upload file and show uploaded file in the html page

Upload page:

<pre>&lt;%= form_for @user, :html =&gt; {:multipart =&gt; true} do |f| %&gt;
  &lt;p&gt;
    &lt;label&gt;My Avatar&lt;/label&gt;
    &lt;%= f.file_field :avatar %&gt;
    &lt;%= f.hidden_field :avatar_cache %&gt;
  &lt;/p&gt;
&lt;% end %&gt;</pre>

View uploaded image

<pre>&lt;%= form_for @user, :html =&gt; {:multipart =&gt; true} do |f| %&gt;
  &lt;p&gt;
    &lt;label&gt;My Avatar&lt;/label&gt;
    &lt;%= image_tag(@user.avatar_url) if @user.avatar? %&gt;
    &lt;%= f.file_field :avatar %&gt;
    &lt;%= f.hidden_field :avatar_cache %&gt;
  &lt;/p&gt;
&lt;% end %&gt;</pre>

Step 8: Now comes the most important part. Setting up fog. Now if you follow the documentation on  <a title="Carrierwave" href="https://github.com/jnicklas/carrierwave" target="_blank">Carrierwave</a> then you will run into issue(**I will explain the issue and fix below**). The wiki page said create a file **fog.rb **in the **lib/carrierwave/storage/fog.rb **and that&#8217;s what I did. I created the file with the contents below.

<pre>CarrierWave.configure do |config|
  config.fog_credentials = {
    :provider               =&gt; 'AWS',       # required
    :aws_access_key_id      =&gt; 'xxx',       # required
    :aws_secret_access_key  =&gt; 'yyy',       # required
    :region                 =&gt; 'eu-west-1'  # optional, defaults to 'us-east-1'
  }
  config.fog_directory  = 'name_of_directory'                     # required
  config.fog_host       = 'https://assets.example.com'            # optional, defaults to nil
  config.fog_public     = false                                   # optional, defaults to true
  config.fog_attributes = {'Cache-Control'=&gt;'max-age=315576000'}  # optional, defaults to {}
end</pre>

Now before you start you need to have a S3 account on <a title="Amazon S3" href="http://aws.amazon.com" target="_blank">Amazon S3</a>. So get your Amazon access key and secret access key. For example mine was &#8230;. hehehe no I am not going to share my access keys with you :-). Anyway if you forgot to note down your access key and incase you are wondering where I can find that and are guessing that it will be on S3 Dashboard then you are mistaken just like me. You can find that on your account settings &#8211;> Security credentials.

[<img class="alignnone size-medium wp-image-579" title="Screen shot 2012-06-03 at 12.26.01 AM" src="http://javahabit.com/wp-content/uploads/2012/06/screen-shot-2012-06-03-at-12-26-01-am1.png?w=300" alt="" width="300" height="102" />][1]

So after you have noted down your key and access key. Go ahead create a bucket on S3. A bucket is nothing but a directory. It&#8217;s just a fancy shimancy name for directory that Amazon came up with. You can further create sub directories.

Now coming back to the meaty part and **fog.rb **file. I updated the below fields in the **fog.rb**

<pre>:aws_access_key_id      =&gt; 'xxx',       # required
    :aws_secret_access_key  =&gt; 'yyy',       # required</pre>

I commented out the below lines as they are optional

<span style="color:#888888;">#:region                 => &#8216;eu-west-1&#8217;  # optional, defaults to &#8216;us-east-1&#8217;</span>

I was not sure what was my region so if you are not sure as well then go ahead and comment it.

<span style="color:#888888;">#config.fog_host = &#8216;https://s3.amazonaws.com&#8217; # optional, defaults to nil</span>
  
 <span style="color:#888888;">#config.fog_public = true # optional, defaults to true</span>

If you leave <span style="color:#888888;"><strong>config.fog_host </strong><span style="color:#000000;">to https://s3.amazonaws.com then I ran into issues which said &#8211;</span></span>

<span style="color:#888888;"><span style="color:#000000;"><strong><span style="color:#808080;"> &#8220;LoadError (Expected /Users/dinesharora/Desktop/Mydocument/ruby-proj/album/app/uploaders/image_uploader.rb to define ImageUploader):&#8221;</span></strong></span></span>

<span style="color:#000000;">So I commented that field. </span>

The next part that I was not sure about was how to tell fog which folder or directory I want to upload my files. I had created a bucket(directory) called **myalbums **and had created a sub folder called devlopment.

So I updated

config.fog_directory  = &#8216;**myalbums/development**&#8216;, which did not work. The right way to do is

config.fog_directory  = &#8216;**myalbums&#8217;** and also in **ImageUploader  **update the line

**def store_dir**
  
 **&#8220;development/uploads/#{model.class.to\_s.underscore}/#{mounted\_as}/#{model.id}&#8221;**
  
 **end**

That&#8217;s it. Now just start the server and start uploading, that&#8217;s what the forums said but as it always happens with me(nothing works for me the first time) I ran into error(as I mentioned earlier that you will if you create the **fog.rb** in lib/carrierwave/storage/ folder) which said &#8211;

**ActionController::RoutingError (uninitialized constant CarrierWave::Storage::Fog):**
  
 **app/uploaders/image_uploader.rb:11:in \`<class:ImageUploader>&#8217;**
  
 **app/uploaders/image_uploader.rb:3:in \`<top (required)>&#8217;**
  
 **app/models/photo.rb:10:in \`<class:Photo>&#8217;**
  
 **app/models/photo.rb:1:in \`<top (required)>&#8217;**
  
 **app/controllers/photo_controller.rb:1:in \`<top (required)>&#8217;**

To get rid of this error, just copy the file in **config/initializers **and now I could finally say &#8211; **That&#8217;s it!!!! 🙂**

~~~ Cheers!

 [1]: http://javahabit.com/wp-content/uploads/2012/06/screen-shot-2012-06-03-at-12-26-01-am1.png