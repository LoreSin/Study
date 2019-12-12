# Tensor board

    기본적인 절차 (코드에 추가)

## 코드작업

1. writer 생성 (저장폴더경로)
2. 수집할 변수들을 기록
3. merge 함수 생성 (변수들을 가져오는 과정)
4. sess 에서 merge 함수를 실행, summary 값 가져옴
5. summary 값을 writer 로 기록

```py
# initialize
sess = tf.Session()
sess.run(tf.global_variables_initializer())

# tensorboard
writer = tf.summary.FileWriter('./log/xavier', sess.graph) # 1
# ./log/xavier  는 xavier 폴더내에 데이터를 저장합니다.

tf.summary.scalar("cost",cost)  # 2
tf.summary.scalar("accuracy",accuracy)  # 2
merged_summary = tf.summary.merge_all()  # 3

# train my model
for epoch in range(training_epochs):
    avg_cost = 0
    total_batch = int(mnist.train.num_examples / batch_size)

    for i in range(total_batch):
        batch_xs, batch_ys = mnist.train.next_batch(batch_size)
        feed_dict = {X: batch_xs, Y: batch_ys}
        summary, acc, c, _ = sess.run([merged_summary, accuracy, cost,  optimizer], feed_dict=feed_dict)  # 4
        avg_cost += c / total_batch
        writer.add_summary(summary, global_step=epoch * total_batch + i)  # 5

```

## 실행방법

>tensorboard --logdir={폴더명}

로그를 저장한 저장경로의 위에서 실행합니다. 위 샘플의 경우 **tensorboard --logdir=.log** 로 하면 됩니다.
실행한 로그에서 나온 주소및 포트로 크롬을 실행해서 접속합니다.
localhost:6006 <== 통상적으로 6006 port 이기 때문에, 대체로 이 주소입니다. 

로그 폴더내의 각 폴더단위로 그래프가 만들어집니다.


