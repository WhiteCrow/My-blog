---
layout: post
title: "Polymorphism and Duck Type in Ruby"
description: ""
category: [technology]
tags: [Ruby]
---
{% include JB/setup %}

Note：some codes are sourced by《Refactoring（Ruby Edition）》

In a static language，design pattern can decouple or put off conditional logic（if，else，switch，case……）.So let us look at what ruby do that only use polymorphism

    class Rental
      def charge
          result = 0
          case movie.price_code
          when Movie::REGULAR
              result += 2
              result += (days_rented -2) * 1.5 if     days_rented > 2
          when Movie::New_RELEASE
              result += days_rented * 3
          when Movie::CHILDRENS
              result += 1.5
              result += (days_rented - 3) * 1.5 if days_rented > 3
          end
          result
      end
    end
    #You can look at the "charge" method should belongs to Movie class.And Movie class inhert Rental class:

    class Movie
      def charge
          result = 0
          case movie.price_code
          when Movie::REGULAR
              result += 2
              result += (days_rented -2) * 1.5 if days_rented > 2
          when Movie::New_RELEASE
              result += days_rented * 3
          when Movie::CHILDRENS
              result += 1.5
              result += (days_rented - 3) * 1.5 if days_rented > 3
          end
          result
      end
    end

