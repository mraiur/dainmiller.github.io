---
published: true
title: Validating the FormKeep API
layout: post
---
In order to verify that GET `/api/forms` serves JSON in the format our client expects, we’ll assert that it successfully validates against a particular JSON schema:


describe "GET /api/forms" do
  it "returns the user's forms" do
    user = create(:user)
    form = create(:form, user: user)

    create(:form)

    json_get "/api/forms", api_token: user.api_token

    expect(response).to be_successful
    expect(response).to match_response_schema("forms-many")
  end
end