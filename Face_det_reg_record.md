# v0.1 2019-6-12
    MTCNN + ArcFace
    
    angle of face [-45,90]  distance of face 0~2m
# v0.2 2019-6-19
    RetinaFace + ArcFace
    
    angle of face [-90,90] distance of face over 3m
# v0.3 2019-8-13
    adjust scale from [720, 1280] to [480, 720]; close tta
    
    time : from 0.27+0.08 to 0.12+0.06
# v0.4 2019-8-16
    add filter small face(100*100) and side face(the x_loc of nose out of two eyes x_loc)
