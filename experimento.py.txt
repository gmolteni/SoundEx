import musicalbeeps
import pyaudio
import numpy as np
import warnings

player = musicalbeeps.Player(volume = 0.3,
                            mute_output = False)

warnings.filterwarnings("ignore", category=DeprecationWarning)


"""
# 1002 1002 1102 1002 1297 1225
# 1002 1002 1102 1002 1469 1378
#                     1569 1378

print(1837/1002*440)
print(2200/1002*440)
print(1696/1002*440)
print(1378/1002*440)
print(1297/1002*440)
print(1102/1002*440)
print(1837/1002*440)
print(1837/1002*440)
print(1696/1002*440)
print(1378/1002*440)
print(1469/1002*440)
print(1297/1002*440)




#print(1002/1002*440)
#print(1102/1002*440)
#print(1297/1002*440)
#print(1225/1002*440)
#print(1469/1002*440)
#print(1569/1002*440)
#print(1378/1002*440)



player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("B4", 0.4)
player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("D5", 0.2)
player.play_note("pause", 0.2)
player.play_note("C5#", 0.4)
player.play_note("pause", 0.5)
player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("B4", 0.4)
player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("E5", 0.2)
player.play_note("pause", 0.2)
player.play_note("D5", 0.4)

player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("A4", 0.2)
player.play_note("pause", 0.2)
player.play_note("B5b", 0.2)
player.play_note("pause", 0.2)
player.play_note("F5#", 0.2)
player.play_note("pause", 0.2)
player.play_note("E5", 0.2)
player.play_note("pause", 0.2)
player.play_note("C5#", 0.2)
player.play_note("pause", 0.2)
player.play_note("B4", 0.2)
player.play_note("pause", 0.2)
player.play_note("G5", 0.2)
player.play_note("pause", 0.2)
player.play_note("G5", 0.2)
player.play_note("pause", 0.2)
player.play_note("F5#", 0.2)
player.play_note("pause", 0.2)
player.play_note("E5b", 0.2)
player.play_note("pause", 0.2)
player.play_note("E5", 0.3)
player.play_note("pause", 0.2)
player.play_note("D5", 0.3)
player.play_note("pause", 0.2)


exit()
"""

648
787
848
1002
1050
1160
1297
1050
816
1102
1297






CHUNK = 4096 # number of data points to read at a time
RATE = 44100 # time resolution of the recording device (Hz)

p=pyaudio.PyAudio() # start the PyAudio class
stream=p.open(format=pyaudio.paInt16,channels=1,rate=RATE,input=True,
              frames_per_buffer=CHUNK) #uses default input device

# create a numpy array holding a single read of audio data
for i in range(10000): #to it a few times just to see
    data = np.fromstring(stream.read(CHUNK),dtype=np.int16)
    #print(data)

    positivo = 0
    negativo = 0
    ultimo   = 0

    histograma = {}

    for e in data:
        if (e>0 and ultimo ==-1):
            #print("Negativo", str(negativo))
            x=str(negativo)
            if x in histograma.keys():
                histograma[x]=histograma[x]+1
            else:
                histograma[x]=1
            negativo = 0


        if (e<0 and ultimo ==1):
            #print("Positivo", positivo)
            x=str(positivo)
            if x in histograma.keys():
                histograma[x]=histograma[x]+1
            else:
                histograma[x]=1
            positivo = 0

        if e >0 :
            positivo +=1
            ultimo = 1
        if e<0:
            negativo +=1
            ultimo = -1


    max = 0
    tmax = 0
    for x in histograma.keys():
        if histograma[x]>max:
            max = histograma[x]
            tmax = x

    t = 2*int(tmax)*(1/44100)
    f=0
    if x !=0:
        f=1/t
    if f < 3000:
        print(f)


# close the stream gracefully
stream.stop_stream()
stream.close()
p.terminate()

# -- feliz cumple --
# 1002 1002 1102 1002 1297 1225
# 1002 1002 1102 1002 1469 1378
#                     1569 1378


# To play an A on default octave n°4 for 0.2 seconds
#player.play_note("A", 0.2)

# To play a G flat on octave n°3 for 2.5 seconds
#player.play_note("G3b", 2.5)

# To play a F sharp on octave n°5 for the default duration of 0.5 seconds
#player.play_note("F5#")

# To pause the player for 3.5 seconds
#player.play_note("pause", 3.5)


