### mongodb 批量删除，批量写入demo

```javascript
const userSchema = new mongoose.Schema({
    nickname: {
        type: String,
        required: true
    },
    mobilephone: {
        type: String,
        required: true
    }
}, {
    collection: 'user'
});

const userModel = mongoose.model('User', userSchema);

class User {
    constructor(user) {
        this.nickname = user.nickname;
        this.mobilephone = user.mobilephone;
    }

    save(cb) {
        const user = {
            nickname: this.nickname,
            mobilephone: this.mobilephone
        };
        const newUser = new userModel(user);

        newUser.save(function (err, user) {
            if (err) {
                return cb(err);
            }
            cb(null, user);
        });
    };

    static get(mobilephone, cb) {
        userModel.findOne({
            mobilephone: mobilephone
        }, function (err, user) {
            if (err) {
                return cb(err);
            }
            cb(null, user);
        });
    };

    //批量删除
    static  delUser(delArray, cb) {
        userModel.remove({
            "_id": {$in: delArray}
        }, function (err, tagId) {
            if (err) {
                return cb(err); //错误，返回错误信息
            }
            cb(null, tagId);
        });
    };

    //批量写入
    static saveUsers(array, cb) {
        userModel.collection.insert(array, function (err, arr) {
            if (err) {
                return cb(err);
            }
            cb(null, arr);
        });
    };

};
```
