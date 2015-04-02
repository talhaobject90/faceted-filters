class HomeController < ApplicationController
  
  around_filter :shopify_session, :except => 'welcome'
  
  def welcome
    current_host = "#{request.host}#{':' + request.port.to_s if request.port != 80}"
    @callback_url = "http://#{current_host}/login"
  end
  
  def index
     if params[:id]
	shop = ShopifyAPI::Shop.current
	product = ShopifyAPI::Product.find(params[:id])
	status = "#{product.title} now available for #{product.price_range} at #{shop.name} http://#{shop.domain}/products/#{product.handle}"
	redirect_to = "http://twitter.com/home?status=#{status}"
	else
    # get 10 products
    @products = ShopifyAPI::Product.find(:all, :params => {:limit => 10})

    # get latest 5 orders
    @orders   = ShopifyAPI::Order.find(:all, :params => {:limit => 5, :order => "created_at DESC" })
	end
  end
  
end
