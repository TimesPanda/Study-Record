#### 1、项目调用音频无法创建对象
```
java.io.IOException: could not create AudioData object
```
```
【原有的写法】
public class MusicPlay {
	  private AudioStream as; // 单次播放声音用  
	  ContinuousAudioDataStream cas;// 循环播放声音  
	  
	    // 构造函数  
	    public MusicPlay(InputStream input) {  
	        try {
	            // 打开一个声音文件流作为输入
	            as = new AudioStream(input);
	            //as = new AudioStream(Thread.currentThread().getContextClassLoader().getResourceAsStream("F:\\dev\\sts-workspace\\Knights\\resource\\music\\BGM.wav"));
	        } catch(FileNotFoundException e) {
	            // TODO Auto-generated catch block  
	            e.printStackTrace();
	        } catch(IOException e){  
	            // TODO Auto-generated catch block  
	            e.printStackTrace();
	        }  
	    }  

	    // 循环播放 开始  
	    public void continuousStart() {  
	        // Create AudioData source.  
	        AudioData data = null;  
	        try {
	        		data = as.getData();  //（这里会出现：java.io.IOException: could not create AudioData object）
	        } catch(IOException e) {  
	            // TODO Auto-generated catch block  
	            e.printStackTrace();  
	        }  
	        // Create ContinuousAudioDataStream.  
	        cas = new ContinuousAudioDataStream(data);  
	        // Play audio.  
	        AudioPlayer.player.start(cas);  
	    }
}
```
```
【解决办法】
 Clip clip = AudioSystem.getClip();
 AudioInputStream inputStream = AudioSystem.getAudioInputStream(SoundManager.class.getResourceAsStream("C://temp/my.mp3"));
 clip.open(inputStream);
 clip.start(); 
```

#### 2、解决audio - java.io.IOException: mark/reset not supported
```
【出现问题的原因】
FileInputStream则没有重写父类InputStream的这两个方法，其不具有mark和reset方法的能力
```
```
【解决办法】
InputStream audioSrc = getClass().getResourceAsStream("mySound.au");
//需要将InputStream再转一下
InputStream bufferedIn = new BufferedInputStream(audioSrc);
AudioInputStream audioStream = AudioSystem.getAudioInputStream(bufferedIn);
```

#### 3、如何在Java中播放.wav文件（循环）
```
Clip clip = AudioSystem.getClip();
clip.open(AudioSystem.getAudioInputStream(new URL(filename)));
clip.start();
clip.loop(Clip.LOOP_CONTINUOUSLY);
```

#### 4、JavaSE项目获取项目路径
```
Swing项目，如果导出或演示的时候，会切换文件夹路径，因此需要动态获取项目本身路径，如下代码即可：
public static String filePath =  System.getProperty("user.dir");
```
