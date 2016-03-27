require 'base64'
require 'json'
require 'uri'
require 'httpclient'
require 'dotenv'

namespace :vision do

  desc 'Unspecified feature type.'
  task :unspecified, [:image_file] do |task, args|
    GCP::CloudVision.new.request('TYPE_UNSPECIFIED', args.image_file)
  end

  desc 'Run face detection.'
  task :face, [:image_file] do |task, args|
    GCP::CloudVision.new.request('FACE_DETECTION', args.image_file)
  end

  desc 'Run landmark detection.'
  task :landmark, [:image_file] do |task, args|
    GCP::CloudVision.new.request('LANDMARK_DETECTION', args.image_file)
  end

  desc 'Run logo detection.'
  task :logo, [:image_file] do |task, args|
    GCP::CloudVision.new.request('LOGO_DETECTION', args.image_file)
  end

  desc 'Run label detection.'
  task :label, [:image_file] do |task, args|
    GCP::CloudVision.new.request('LABEL_DETECTION', args.image_file)
  end

  desc 'Run OCR.'
  task :text, [:image_file] do |task, args|
    GCP::CloudVision.new.request('TEXT_DETECTION', args.image_file)
  end

  desc 'Run various computer vision models to compute image safe-search properties.'
  task :safe_search, [:image_file] do |task, args|
    GCP::CloudVision.new.request('SAFE_SEARCH_DETECTION', args.image_file)
  end

  desc 'Compute a set of properties about the image (such as the image\'s dominant colors).'
  task :image_properties, [:image_file] do |task, args|
    GCP::CloudVision.new.request('IMAGE_PROPERTIES', args.image_file)
  end

end

module GCP
  class CloudVision
    def request(feature_type, image_file)
      image = open_or_download image_file
      base64_image = base64_encode image
      request_body = create_request_body feature_type, base64_image
      response = execute_cloud_vision request_body
      puts response
    end

    private

    def create_request_body(feature_type, base64_image)
      {
        requests: [{
          image: {
            content: base64_image
          },
          features: [
            {
              type: feature_type,
              maxResults: 10
            }
          ]
        }]
      }.to_json
    end

    def execute_cloud_vision(body)
      HTTPClient.new.post_content(api_url, body, 'Content-Type' => 'application/json')
    end

    def base64_encode(image)
      Base64.strict_encode64(image)
    end

    def open_or_download(image_file)
      if URI.extract(image_file).first.nil? then
        File.new(image_file, 'rb').read
      else
        HTTPClient.new.get_content(image_file)
      end
    end

    def api_url
      Dotenv.load
      "https://vision.googleapis.com/v1/images:annotate?key=#{ENV['GCP_API_KEY']}"
    end

  end
end

