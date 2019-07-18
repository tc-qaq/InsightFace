# [RetinaFace](https://github.com/deepinsight/insightface/tree/master/RetinaFace)
  
  [Paper](https://arxiv.org/abs/1905.00641)

# Arch

Conv0(out_c=8, in_c=1, kernerl=3,pad=1,stride=2)-BN()-ReLU()
Conv1(out_c=8, in_c=8, kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv2(out_c=16,in_c=8, kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv3(out_c=16,in_c=16,kernerl=3,pad=1,stride=2)-BN()-ReLU()
Conv4(out_c=32,in_c=16,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv5(out_c=32,in_c=32,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv6(out_c=32,in_c=32,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv7(out_c=32,in_c=32,kernerl=3,pad=1,stride=2)-BN()-ReLU()
Conv8(out_c=64,in_c=32,kernerl=1,pad=0,stride=1)-BN()-ReLU()

Conv9(out_c=64,in_c=64,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv10(out_c=64,in_c=64,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv11(out_c=64,in_c=64,kernerl=3,pad=1,stride=2)-BN()-ReLU()
Conv12(out_c=128,in_c=64,kernerl=1,pad=0,stride=1)-BN()-ReLU()

Conv13(out_c=128,in_c=128,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv14(out_c=128,in_c=128,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv15(out_c=128,in_c=128,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv16(out_c=128,in_c=128,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv17(out_c=128,in_c=128,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv18(out_c=128,in_c=128,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv19(out_c=128,in_c=128,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv20(out_c=128,in_c=128,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv21(out_c=128,in_c=128,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv22(out_c=128,in_c=128,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv23(out_c=128,in_c=128,kernerl=3,pad=1,stride=2)-BN()-ReLU()
Conv24(out_c=256,in_c=128,kernerl=1,pad=0,stride=1)-BN()-ReLU()
Conv25(out_c=256,in_c=256,kernerl=3,pad=1,stride=1)-BN()-ReLU()
Conv26(out_c=256,in_c=256,kernerl=1,pad=0,stride=1)-BN()-ReLU()

rf_c3_latteral(conv1x1,out=64)-BN-ReLU   ------------------------------- followed by Conv26

rf_c3_det_conv1(conv3x3,out=32)-BN
rf_c3_det_context_conv1(conv3x3,out=16)-BN-ReLU
rf_c3_det_context_conv2(conv3x3,out=16)-BN
rf_c3_det_context_conv3_1(conv3x3,out=16)-BN-ReLU
rf_c3_det_context_conv3_2(conv3x3,out=16)-BN
Concat(rf_c3_det_context_conv1,rf_c3_det_context_conv2,rf_c3_det_context_conv3_2)-ReLU
face_rpn_cls_score_stride32(conv1x1,out=4)-Reshape-Softmax
face_rpn_bbox_pred_stride32(conv1x1,out=8)
face_rpn_landmark_pred_stride32(conv1x1,out=20)


rf_c2_lateral(conv1x1,out=64)-BN-ReLU   ---------------------------------- followed by Conv22

rf_c3_UpSampling(2)-Crop()-elemwiseAdd()
rf_c2_aggr(conv3x3,out=64)-BN-ReLU
rf_c2_det_conv1(conv3x3,out=32)-BN
rf_c2_det_context_conv1(conv3x3,out=16)-BN-ReLU
rf_c2_det_context_conv2(conv3x3,out=16)-BN
rf_c2_det_context_conv3_1(conv3x3,out=16)-BN-ReLU
rf_c2_det_context_conv3_2(conv3x3,out=16)-BN
Concat(rf_c2_det_context_conv1,rf_c2_det_context_conv2,rf_c2_det_context_conv3_2)-ReLU
face_rpn_cls_score_stride16(conv1x1,out=4)-Reshape-Softmax
face_rpn_bbox_pred_stride16(conv1x1,out=8)
face_rpn_landmark_pred_stride16(conv1x1,out=20)


rf_c1_lateral(conv1x1,out=64)-BN-ReLU   ---------------------------------- followed by Conv10

rf_c2_upsampling(2)-Crop()-elemwiseAdd()
rf_c1_aggr(conv3x3,out=64)-BN-ReLU
rf_c1_det_conv1(conv3x3,out=32)-BN
rf_c1_det_context_conv1(conv3x3,out=16)-BN-ReLU
rf_c1_det_context_conv2(conv3x3,out=16)-BN
rf_c1_det_context_conv3_1(conv3x3,out=16)-BN-ReLU
rf_c1_det_context_conv3_2(conv3x3,out=16)-BN
Concat(rf_c1_det_context_conv1,rf_c1_det_context_conv2,rf_c1_det_context_conv3_2)-ReLU
face_rpn_cls_score_stride8(conv1x1,out=4)-Reshape-Softmax
face_rpn_bbox_pred_stride8(conv1x1,out=8)
face_rpn_landmark_pred_stride8(conv1x1,out=20)

