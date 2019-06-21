# [InsightFace](https://github.com/deepinsight/insightface)

# Pipeline

image->MTCNN->ArcFace

# MTCNN pipeline
 
image->PNet->RNet->ONet

    PNet: gen anchor for bg and face
    
    RNet: refine anchor and classificare face
    
    ONet: gen landmark
    
# ArcFace

   Backbone: input_layer: Conv3-BN-PReLU
               
             body:  Bottlenecks(3,4,14,3)
             
             output_layer: BN-Dropout-Flatten-FC-BN
             
   ArcFace head: cos_theta -> cos_theta_m
                 cond_mask -> keep
                 output
