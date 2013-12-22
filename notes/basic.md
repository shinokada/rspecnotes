# Rspec basics

## describe and context

Use `describe` to describe methods, class methods and instance methods.  Use context to test states for example when 
describing a context, start its description with "when" or "with".

## expect not should

[transpec](https://github.com/yujinakayama/transpec#supported-conversions)

    # old
    1.should == 1
    1.should < 2
    Integer.should === 1
    'string'.should =~ /^str/
    [1, 2, 3].should =~ [2, 1, 3]
    account.balance.should == 0
    logger.should_receive(:account_closed).with(account)
    lambda { account.renew }.should_not raise_error(Account::RenewalError)

    # new
    expect(1).to eq(1)
    expect(1).to be < 2
    expect(Integer).to be === 1
    expect('string').to match(/^str/)
    expect([1, 2, 3]).to match_array([2, 1, 3])
    expect(account.balance).to eq(0)
    expect(logger).to receive(:account_closed).with(account)
    expect { account.renew }.not_to raise_error

## `it` and `specify` are identical methods



