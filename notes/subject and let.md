# Subject and let
Collection of articles about Rspec subject and let.

[Dry up your Rspec files with subject & let blocks](http://benscheirman.com/2011/05/dry-up-your-rspec-files-with-subject-let-blocks/)

Good example to use `subject` and `let`. `its` will be [moved into an external gem](https://gist.github.com/myronmarston/4503509)

    # original example

    require 'spec_helper'
     
    describe Card do
      describe "#new" do
        describe "Two of Hearts" do
          it "has a value of 2" do
            card = Card.new("2H")
            card.value.should equal(2)
          end
        end
    ...
    ...

    #improved example

    require 'spec_helper'
     
    describe Card do
      subject do
        Card.new(card_type)
      end
      
      describe "#value" do  
        context "Two of Hearts" do
          let(:card_type) { "2H" }
          its(:value) { should == 2 }
        end
    ...
    ...



[Spec smell: explicit use of subject](http://blog.davidchelimsky.net/blog/2012/05/13/spec-smell-explicit-use-of-subject/)

## Implicit subject

    describe Article do
      it { should validate_presence_of(:title) }
    end


RSpec knows that the first argument to describe is the Article class, it can store a similar block in the background as a default, implicit subject declaration.

## Explicit subject


    describe AmericanCitizen do
      context "18 years of age" do
        subject { Person.new(:birthdate => 18.years.ago) }
        it { should     be_able_to(:vote)   }
        it { should     be_able_to(:enlist) }
        it { should_not be_able_to(:drink)  } # srsly?
      end
    end

## Named subject

    describe CheckingAccount, "with a non-zero starting balance" do
      subject(:account) { CheckingAccount.new(Money.new(50, :USD)) }
      it { should_not be_overdrawn }
      it "has a balance equal to the starting balance" do
        account.balance.should eq(Money.new(50, :USD))
      end
    end


## [Use let to an instance variable](http://stackoverflow.com/questions/5359558/when-to-use-rspec-let)



[let and let!](https://www.relishapp.com/rspec/rspec-core/v/2-6/docs/helper-methods/let-and-let)


    $count = 0
    describe "let" do
      let(:count) { $count += 1 }
    
      it "memoizes the value" do
        count.should == 1
        count.should == 1
      end
    
      it "is not cached across examples" do
        count.should == 2
      end
    end
