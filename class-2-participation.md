``` r
data("gapminder")
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

``` r
ggplot(data = gapminder, mapping = aes(x = year, y = pop, color = continent)) +
  geom_point()
```

![](class-2-participation_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
#or do it this way to layer onto the graph
#ggplot() +
 # geom_point(data = gapminder, mapping = aes(x = year, y = pop)
```

``` r
#aggregate by continent

gapminder %>%
  group_by(year, continent) %>%
  summarise(pop=sum(pop))%>%
  ggplot(data =., mapping = aes(x=year, y = pop, color = continent)) +
  geom_point()+
  scale_y_log10()
```

    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))
    
    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))
    
    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))
    
    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))
    
    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))
    
    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))
    
    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))
    
    ## Warning in summarise_impl(.data, dots, environment(), caller_env()):
    ## integer overflow - use sum(as.numeric(.))

    ## Warning: Removed 8 rows containing missing values (geom_point).

![](class-2-participation_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

facet grid = facet on two variables facet wrap = only specify one
variable

``` r
gapminder %>%
  filter(continent == "Asia") %>%
ggplot(data = ,, mapping = aes(x = year, y = gdpPercap, colour = country)) +
  geom_point() +
  facet_wrap(~continent)
```

![](class-2-participation_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(data = gapminder, aes(x = gdpPercap, y = lifeExp, colour = continent, size = pop))+
  geom_point() +
  scale_x_log10() +
  stat_smooth(method = "lm")
```

![](class-2-participation_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

changing mapping for population

``` r
gapminder %>%
  filter(continent == "Europe") %>%
  group_by(country) %>%
  summarise(gdpPercap = mean(gdpPercap),
            lifeExp = mean(lifeExp))%>%
ggplot(data = ., aes(x = gdpPercap, y = lifeExp, shape = country))+
  geom_point() +
  scale_x_log10() +
  stat_smooth(method = "lm")
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values
    ## because more than 6 becomes difficult to discriminate; you have
    ## 30. Consider specifying shapes manually if you must have them.

    ## Warning: Removed 24 rows containing missing values (geom_point).

![](class-2-participation_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp))+
  geom_point(aes(color = continent), alpha = .3)+
  scale_x_log10() +
  stat_smooth(method = "lm", mapping = aes(color = continent))
```

![](class-2-participation_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp))+
  geom_point(alpha = .3)+
  scale_x_log10() +
  stat_smooth(method = "lm")+
  facet_wrap(~continent) +
  xlab("GDP Per Capita") +
  ylab("Life Expectancy") +
  ggtitle("Life Expectancy By GDP per Capita", subtitle = "Faceted By Continent")
```

![](class-2-participation_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
ggplot(data = gapminder, mapping = aes(x = gdpPercap, y = lifeExp))+
  geom_point(alpha = .3)+
  scale_x_log10() +
  stat_smooth(method = "lm")+
  facet_wrap(~continent) +
  xlab("GDP Per Capita") +
  ylab("Life Expectancy") +
  ggtitle("Life Expectancy By GDP per Capita", subtitle = "Faceted By Continent") +
  coord_flip()
```

![](class-2-participation_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
gapminder %>%
ggplot(data = ., mapping = aes(x = continent, y = lifeExp))+
  stat_summary(fun.ymin = min, 
               fun.ymax = max, 
               fun.y = median,
               alpha = .9) +
  geom_point() + 
  coord_flip() +
  theme_economist()
```

![](class-2-participation_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->
