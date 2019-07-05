# weixinpay
微信支付 node.js sdk

    const weixinpay = new Weixinpay(
       {
          appid: '****',
          mch_id: '****',
          partner_key: '******',
          pfx: fs.readFileSync('证书路径')
       },
       process.env.NODE_ENV != 'producton' // true 为沙箱环境
     );
      // 统一下单
      const type = "app";
      const result = await weixinpay.createUnifiedOrder({
                body: "好打的一个商品" ,
                out_trade_no: "201900000020303",
                total_fee: process.env.NODE_ENV == 'production' ? "真实金额" : 101,
                spbill_create_ip: "客户端IP",
                notify_url: `${process.env.NODE_ENV ==  'production'?'http://服务器地址':'http://测试服务器地址'}/接口路径`,
                trade_type: type,// 支付类型 app 扫码等
                product_id: "productId"
        });
        if(type=="app"){
          res.json({
              status: 'success',
              msg: channel,
              data: weixinpay.signForApp(result) // app 支付签名后返回给客户端
          });
        }
            
